---
layout: post
title: Tracking Newsfeed activity
excerpt_separator: <!--more-->
---


Let's imagine a user browsing Facebook's Newsfeed. 
This post describes how I would track basic Newsfeed user activity and design schemas in Redshift.

<!--more-->


`feed_init` triggers when the user lands on a web page or app screen with a Newsfeed. 

| Field | Type | Description |
|---|---|---|
| user_id | uuid | id of the user. Distribution key in Redshift. |
| ts | timestamp | wallclock time when the event triggered. Sort key |
| session_id | uuid | each feed load generates a unique session_id |


`feed_show_story` triggers every time a story is displayed to the user. 

| Field | Type | Description |
|---|---|---|
| user_id | uuid | distribution key |
| ts | timestamp | sort key |
| session_id | uuid | each feed load generates a unique session_id |
| story_id | timestamp | uuid of the story shown |
| story_index | timestamp | index of the story in the feed, start at zero |

Both events are sent to and stored in Redshift, one table per event.


So far we only have raw logs. Analysts prefer sessions, so let's give them `feed_sessions`:

| Field | Type | Description |
|---|---|---|
| user_id | uuid | distribution key |
| session_start_at | timestamp | sort key |
| session_id | uuid | each feed load generates a unique session_id |
| stories_seen | int | max story index, 0 if none were seen |

This sessionized table comes from an ETL job like this one in Redshift SQL dialect:

```sql
select 
  i.user_id,
  i.ts as session_start_at,
  i.session_id,
  nvl(max(s.story_index),0) as stories_seen
from feed_init i
left join feed_show_story s
  on i.session_id = s.session_id
  and datediff('second', i.ts, s.ts) <= 12*60*60 -- cap sessions to 12h
where i.ts >= '2018-08-01' 
  and i.ts < '2018-08-02'
  and s.ts >= '2018-08-01'
  and s.ts < '2018-08-02 12:00:00' -- extra 12h so as to not cut sessions starting at 23:59
```


In a next post, I'll cover the inefficiency with joining this way on Redshift.
