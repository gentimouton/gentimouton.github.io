---
layout: post
title: Reverse-engineering Netflix CTR tracking
excerpt_separator: <!--more-->
---

This post is an introduction to tracking user behavior on apps and websites. 
It focuses on how Netflix tracks carousel loads and user clicks on movie cards.

<!--more-->

Most data products out there rely on knowing how users interact with the product. 
On Netflix for example, improving recommender systems requires knowing which movies were loaded in which carousel, 
which movie cards were clicked on, which movies started being watched, and if they were watched completely or not. 
Armed with data from the carousel loads and card clicks, 
a data analyst could measure the click-through rate for each movie card presented in the first carousel. 
They could design an AB experiment where they compare different cards, and keep those with the highest click-through rate.

Concretely, carousel loads on the web app are tracked via a HTTP POST request to this endpoint: 
```
https://www.netflix.com/uitracking/users/presentationtracking
```
The client sends a JSON payload indicating location, video_id, carousel number,
position of item in each carousel, image key (thumbnail), and more.

Clicking on the 3rd item of the 5th carousel, the URL to the movie page is:
```
https://www.netflix.com/watch/80170100?trackId=12345678&tctx=5,3,a65ca16f-c4be-4a30-8bd6-f011348a6d1e-161234387
```
I think the ids are: movie number, user id, position of clicked carousel in page, position of clicked item in carousel, and session id. 
They probably have an event fired in the backend, e.g. `recommendations_loaded` with user_id, session id, and list of recs for each carousel. This would allow them to join backend loads with front-end clicks.

### Related
- [Tracking using Google Analytics](https://searchenginewatch.com/sew/how-to/2287906/10-google-analytics-custom-events-that-track-the-untrackable)
- [Google Analytics dev manual](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
