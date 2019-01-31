---
layout: post
title: Future data jobs
excerpt_separator: <!--more-->
---

This is a list of data-related jobs I think are likely to develop in the next 5 to 10 years.

<!--more-->

## Feature scientist

Feature engineering is the art of coming up with useful metrics for a given domain. For example, a movie recommender may improve its performance by including movie budget or measuring sentiment from captions. Having more discriminative metrics improves machine learning models. Today, features come from applied scientists who aren't necessarily domain experts, but are experts at training, testing, and deploying models. Feature scientists will be domain experts, halfway between today's product managers and backend applied scientists. 

One may argue that neural nets make feature engineering obsolete. And although they are currently expensive to train, they will become cheaper. Both may be true, but I think 10 high-signal independent features will still achieve better performance than 100 low-signal quasi-colinear ones.


## Causal scientist

Correlation is not causation. Yet when executives notice big changes month over month, they are often satisfied with a break-down by platform, geo, etc. These breakdowns are descriptive and correlational, but not causational.
For example, 15pp of a 20% month-over-month growth come from mobile in South Korea. Marketing brings up a re-activation email campaign they just ran, a South-Korean employee mentions a big national holiday, and Infrastructure points to the new South-East Asia CDN. How much does each account for the 15pp? Are there synergies?

Today, data scientists and analysts prove causation via simple AB experiments. In the future, causal scientists will design and analyze more complex experiments, eg with factorial designs and surface response. They'll be domain experts too, and will come up with user experiences to reduce between-group variance, like [Netflix's interleaving](https://medium.com/netflix-techblog/interleaving-in-online-experiments-at-netflix-a04ee392ec55). Domain knowledge will also help them hunt for quasi-experiments and apply [diff-in-diff](https://en.wikipedia.org/wiki/Difference_in_differences) and [Causal Impact](https://google.github.io/CausalImpact/CausalImpact.html).


## Applied scientist in recommendation/forecasting/anomaly detection

Anomaly detection, recommenders, and forecasting are machine learning problems found in all business domains. These problems exist today, and have specialists working on them in tech companies. Their awareness will spread to other industries, and so these 3 jobs will become more commonplace.

These specialized applied scientists will develop models using standard techniques and infrastructures. Their models will be served by product/data engineers, or maybe automatically by established infrastructures or services. Think recommender-as-a-service, where your data scientist tweaks the model part of the pipeline. 


## Pipeline engineering director

Data pipelines exist today. They are becoming more and more complex and interdependent. For example, ingesting client event streams into a data lake is a pipeline. So is ETLing operational datastores into that same lake. Linkedin has a metrics pipeline called UMP, which irrigates various internal tools like their experimentation analysis and their reporting. Any machine learning model in production has its own pipeline, ranging from pulling data to training a model, testing it, serving it, or issuing high-frequency trading orders from it. 

Data pipelines will become the backbone of companies, and they will have to become more resilient. Their organization and management practices will probably be specific to a domain, if not to a company. This will result in more director-level roles, maybe mega-architects too.


## Product tracking architect

Today, the most rudimentary product tracking consists of server logs. For example, webservers log client HTTP requests. These include the URL of the page requested and the previous URL where the user came from. These 2 are enough to build user navigation patterns.
However, mobile apps don't request HTML pages, but data from multiple endpoints at once. We want to confidently match multiple endpoint requests to the single user action that triggered them. One solution today is for clients to pass a common uuid to the endpoints they request from. 
Another limitation of webserver tracking is they don't tell how long a user spent on a page or resource. This is crucial for music or video recommenders, who care if a user bounces off the site within 10 seconds after requesting a song, or if they play it nearly until its end. One solution is for the client to fire a heartbeat event every 10 seconds. But on mobile apps, cell coverage can be spotty, and the events may need to be batched. 

These complexities add up to a full-time job. Tracking architects will make sure that tracking is effective, efficient, and consistent across clients. Very much like object-oriented programming in the early 2000s, they will invent and evangelize design patterns to track user behavior more and more elegantly. 
