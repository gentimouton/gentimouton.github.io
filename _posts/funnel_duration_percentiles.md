---
layout: post
title: Summarizing funnel duration via percentiles
excerpt_separator: <!--more-->
---

App users often go through processes involving several steps, like browsing > adding to cart > checking out. 
We want to measure the typical duration of each step and of the whole process.
Averaging durations naively (dividing sum by count) skews towards users who take an abnormally long time to go through a step.
What about using percentiles instead?

<!--more-->

Let's look at some made-up data. Each row is a completed process. 
Cells represent the duration in minutes for the step to happen.

| Step A | Step B | Total duration |
|---|---|---|
| 1 | 2 | 3 |
| 1 | 2 | 3 |
| 1 | 3 | 4 |
| 2 | 2 | 4 |
| 3 | 3 | 6 |

The 80th percentile (or p80) of step A is 2m, step B 3m, and overall process 4m.
Some thoughts:
- Percentiles are not additive, even when there are no noticeable outliers.
- Communicating these numbers is tricky. Readers expect them to match. 
- Averages always add up and match, but don't make sense for bimodal or long-tailed distributions.
- Any mechanism speeding up step B when step A was slow, accentuates the discrepancy.


## FAQ

What about incomplete user funnels, such as adding to cart without ever checking out?
- The longer a step takes, the more likely it is for users to bounce. It's a good idea to measure bounce rate for each step, and show it alongside summarized step durations.

What about averaging capped durations instead?
- Mitigating outliers is a good idea. However justifying a threshold to label data points as outliers vs legit can prove difficult. N standard deviations from mean comes to mind - what should N be? 
