---
layout: post
title: Redshift joins
excerpt_separator: <!--more-->
---

[Redshift](https://aws.amazon.com/redshift/) is a distributed columnar database. 
Columnar databases scale easily by distributing data between nodes in very specific ways.
This typically comes with a cost: joins are expensive, if not impossible.
Redshift is no exception, although it allows a 
[distribution key](https://docs.aws.amazon.com/redshift/latest/dg/t_Distributing_data.html) 
by which to spread records.
This way, joins on distkeys do not require records to be shuffled between nodes, and are somewhat cheap.
Surprisingly, however, joins on distkey _and_ another column currently require a shuffle.


<!--more-->

Let's take the example of tracking Newsfeed user sessions.
The ETL below appends nightly to a `feed_sessions` table.
It pulls from `feed_init` and `feed_show_story`, which both distkey on user_id.

```sql
select 
  i.user_id,
  i.ts as session_start_at,
  i.session_id,
  nvl(max(s.story_index),0) as stories_seen
from feed_init i
left join feed_show_story s
  on i.session_id = s.session_id
  and datediff('second', i.ts, s.ts) <= 12*60*60 
  -- cap sessions to 12h
where i.ts >= '2018-08-01' 
  and i.ts < '2018-08-02'
  and s.ts >= '2018-08-01'
  and s.ts < '2018-08-02 12:00:00' 
  -- extra 12h so as to not cut sessions starting at 23:59
```

When running this query, the 
[optimizer detects](https://docs.aws.amazon.com/redshift/latest/dg/c-the-query-plan.html) 
that `session_id` is the distkey of neither table.
Running an `explain` outputs a super expensive line like this:
> -> XN Hash Join DS_DIST_BOTH (cost=123456.78..234567.89 rows=78901 width=89)

The optimizer does not know that each `session_id` maps to a single `user_id`.
Redshift is not a relational DB, and it does not enforce such subkey constraints.
We could explicitly tell the optimizer to consider the distkey.
However, adding a `and i.user_id = s.user_id` outputs the same query plan.
If it worked, we'd see something like this instead:
> -> XN Merge Join DS_DIST_NONE (cost=0.0..123.45 rows=78901 width=89)


I'm not sure it's a bug or a feature to be added, but I would really like it if the Redshift optimizer considered the distkey when I explicitly write it in a join.


See also this [Yelp presentation](https://youtu.be/GhHXVVFju9Q?t=42m51s) on Redshift distkeys.
