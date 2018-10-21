---
layout: post
title: PPS sampling in Redshift SQL
excerpt_separator: <!--more-->
---

Sampling is often necessary for heavy algorithms to run on large populations.
Sometimes, we want to draw some elements more frequently than others.
For example, we could draw US states proportionally to their population.
In this case, we could use probability-proportional-to-size (PPS) [sampling](https://en.wikipedia.org/wiki/Sampling_%28statistics%29).
This post provides an efficient SQL script to sample 
any number of weighted elements via PPS sampling.

<!--more-->


# Weighted-sampling algorithms

There are [many](https://en.wikipedia.org/wiki/Sampling_(statistics)#Sampling_methods),
and each treats weights differently. 
For example, draw 2 elements from `{a:40, b:30, c:30}`.
- Sampling without replacement: 37% `ab`, 37% `ac`, and 26% `bc`.
See this [link](https://math.stackexchange.com/a/1435631).
- Sampling with replacement: 16% `aa`, 9% `bb`, 9% `cc`, 24% `ab`, 24% `ac`, and 18% `bc`.
- Systematic PPS sampling: 40% of pairs are `ab`, 40% `ac`, and 20% `ac`.

In this post, I only provide SQL code for systematic PPS sampling.


# FAQ

**What are the algorithm's assumptions?**

1. At least one element in the population must have a non-zero weight.
2. The weight of the heaviest element must be strictly less than 1/sample size.
For example, consider drawing 2 elements from `{a:60, b:20, c:20}`. 
`a`'s weight, 60%, is greater than 1/2, ie 50%.
With systematic sampling, the chance of drawing `{b,c}` is actually 0%.

**Why is this algorithm appropriate for Redshift SQL?**

It's both efficient and predictable. 
- Efficient: No cross joins are necessary to draw a sample of any size. 
Space complexity is O(population size).
In the script below, the cross joins are only here to simulate draws.
- Predictable: Sample size is predetermined, unlike with Poisson sampling for example.

**What are the alternatives?**

- Sampling locally in Python or R: With billions of elements, though, 
sampling has to happen within Redshift.
- EMR on a data dump: When the data lives in Redshift, this seems impractical.
- Sampling with replacement: I believe this requires a cross join in Redshift SQL.
The space complexity is O(population size * sample size), which is impractical.
- Not sure how to do sampling without replacement for arbitrary sample sizes in Redshift SQL 
(ie with neither `pivot` nor recursive CTEs).
- [Poisson sampling](https://onlinecourses.science.psu.edu/stat504/node/57/)
might be a good alternative, maybe via a Python UDF in Redshift.

**Any benchmark?**

Sampling 60M elements out of 700M took 13 minutes on a 100-node cluster.
Sampling 40k out of 400k took 7s.

# Redshift SQL snippet

This script simulates 10k draws from a population where each element has a weight.
It respects the weights via systematic PPS sampling.


```sql
with pop as (
-- dummy test data
      select 'a20' as element, 20 as w
union select 'b20' as element, 20 as w
union select 'c20' as element, 20 as w
union select 'd15' as element, 15 as w
union select 'e15' as element, 15 as w
union select 'f05' as element, 5 as w
union select 'g05' as element, 5 as w
union select 'h00' as element, 0 as w
-- -- unit test
--       select 'a40' as element, 40 as w
-- union select 'b30' as element, 30 as w
-- union select 'c30' as element, 30 as w
-- union select 'd00' as element, 0 as w
)

, sample_size_def as (
select 4 as sample_size
)

-- generate integers up to 10k
, digits as (
      select 0 as i
union select 1 as i
union select 2 as i
union select 3 as i
union select 4 as i
union select 5 as i
union select 6 as i
union select 7 as i
union select 8 as i
union select 9 as i
)

, integers as (
select
  d1.i + 10*d2.i + 100*d3.i + 1000*d4.i as n
from digits d1
cross join digits d2
cross join digits d3
cross join digits d4 -- up to 10k
)

, normalized_pop as ( 
-- normalize weights to sum to 1
select element, ratio_to_report(w::float) over() as elem_w from pop
)

, simulations as ( 
-- generate integers and random selection points in [0,1)
-- redshift does not support generate_series(1,10000) as of 2018-10
select 
  random() as selection_point,
  s.sample_size,
  n as sim_id
from integers 
cross join sample_size_def s
limit 10000 -- number of simulations, use limit 1 to subsample once
)

, simulated_shuffles as (
-- in each simulation, order channels randomly
-- cast to bigint because redshift can't mod(decimal, decimal)
select
  sim_id,
  element,
  elem_w,
  selection_point / sample_size as selection_offset,
  1.0 / sample_size as selection_window_width, 
  sum(elem_w) over(
    partition by sim_id 
    order by random() 
    rows between unbounded preceding and current row
    ) as elem_upper_bound,
  -- redshift allows definitions using columns defined earlier in the CTE
  elem_upper_bound - (elem_w) as elem_lower_bound 
from normalized_pop p
cross join simulations s
)

, selected_elements as (
-- select the element whose range contains the selection point
-- watch out for window boundaries (WB)!
select 
  *
from (
select 
  *,
  -- compute selection point in the window where this element starts
  floor(
    elem_lower_bound/selection_window_width
    ) * selection_window_width + selection_offset 
    as selection_point
from simulated_shuffles
) a
where 
  -- captures LB < SP < UB < WB and LB < SP < WB < UB (element crosses boundary)
  ( elem_lower_bound <= selection_point 
    and elem_upper_bound > selection_point )
  -- captures SP < LB < WB < SP+WW < UB (element crosses boundary)
  or ( elem_lower_bound <= selection_point + selection_window_width
    and elem_upper_bound > selection_point + selection_window_width )
)

-- aggregate simulation results
select
  pop.element,
  count(s.sim_id) as times_picked
from pop
left join selected_elements s
  on pop.element = s.element
group by 1
order by 1
```


element|times_picked
|---|---|
a20|8020
b20|8068
c20|8058
d15|5997
e15|5931
f05|1967
g05|1959
h00|0
