---
layout: post
title: The care and feeding of data scientists
excerpt_separator: <!--more-->
---

This post is my notes on a [white paper](https://oreilly-ds-report.s3.amazonaws.com/Care_and_Feeding_of_Data_Scientists.pdf)
by [Michelangelo D'Agostino](https://www.linkedin.com/in/michelangelod/)
and [Katie Malone](https://www.linkedin.com/in/caitlin-malone-46050854/) on managing data scientists.
Overall, the report is a good introduction to the basics of managing DS, providing a bunch of generally-applicable guidelines.
Note however that both authors come from the same company (Civis), and are relatively junior managers 
(5 and 3 years of management experience respectively).

<!--more-->

## 1- Roles and organization

If the team and the company are small, don't overthink roles: everyone is a DS.
Specializations: 
- operational DS focuses on analysis for executives and sales, 
- product DS ships models to product teams,
- engineering DS builds machine learning systems,
- research DS pushes the state of the art.

Possible structures
- centralized: all DS in one team: strong job identity and data culture, but farther from customers.
- distributed: sit next to customer, but isolation and lack mentorship.
- embedded: team of DS for identity, but accountable to customer teams' and attend their standups.

## 2- Recruiting

Since DS like to learn, attract talent by presenting at meetups, blogging, 
guest-teaching at university, or contributing to open source.

Typical questions candidates ask:
- role of DS team in the company
- prioritization and choice of DS projects
- collaboration between DS
- onboarding, performance reviews, career paths, diversity
- tools and tech stack

When starting a team, hire super senior DS, so your second wave of junior DS have mentors.
Pros and cons of junior candidate backgrounds:
- PhD grads from quant fields: self-directed, technically deep, but lack business acumen, slow, and maybe not exposed to ML.
- DS MS or bootcamp: broad but shallow exposure to ML.
- software engineers: strong eng skills, less stats or business.
- data analysts: good at business, lacks eng skills.

Treat recruiting as exercise in community building.


## 3- Interviewing

Job posting: Start from career path doc, or ask your team what skills are essential vs can be picked up, 
or write bullet points for each of these 3 families of reqs: 
- knowledge (what they know), 
- skills (what they can do), 
- dispositions (attitude).

Tasks and tips
- Ask concrete (not hypothetical) questions, eg "tell me of a time when you had to learn something on your own".
- Make technical screens as similar as possible to the actual job.
- Whiteboard on given dataset + business problem, and brainstorm "imagine we are team mates".
- Pair program, 
- Debug code snippet, or walk through their Github code
- Teach something you are an expert at to diverse crowd,
- Take-homes: due in 1 week, spend only a few hours on it. Can use it as prompt in onsite interview.

Two great candidates: how to break the tie:
- New or small teams: probably need to build pipelines, prefer engineer over statistician.
- Senior DS spend more time maintaining models and answering ad-hoc questions: hire junior DS to take over.

Feedback diversity and avoiding groupthink: 
- Diverse panel.
- Keep candidate feedback private until sync. 
- In sync, highest-status interviewer goes last.

Onboarding:
- Based on their knowledge gap, build development plan and career path.
- 30-day plan to learn their way around: coffee with everyone on list, fix 3 bugs, and give presentation.
- 90-day plan to reach cruising speed, or correct course.


## 4- Keeping things interesting

Lack of challenge and learning are top 2 reasons for DS to change job.
Fear of missing out - "my company isn't doing any cool ML or Spark" - leads to loathing of management.
Solutions: 
- hire DS who want to have impact, not who want cool new toys.
- journal club, eg over lunch. White paper has list of a dozen sources, eg [Morning Paper](https://blog.acolyer.org/).
- watch talks, eg from PyData
- Google's 20% does not work - too hard to pull people for a half-day off their usual work. Instead, hack weeks with clear deliverable (eg blog, prototype, notebook, open source bugfix), light accountability (daily check-in to hack week buddy, final presentation).
- allow attending conferences or meetups.


## 5- Agile and OKR

Agile started with core principles, then became codified, 
and it now has its own processes like sprint planning and retros.
Too much process can turn DS away, decrease creativity, etc.
Solution: go back to original Agile principles:
- Individuals and interactions over processes and tools -> talk to customers to understand the business and their problem.
- Customer collaboration over contract negotiation -> frequent incremental presentations to customers.
- Responding to change over following a plan -> learn as you go.

Objectives (the final goal) and Key Results (steps towards goal).
Decline each KR in 3 (quality X achievability) levels: decent and definitely achievable, great and unlikely, and amazing but impossible.
Example:
- Objective: surprise and delight the customer with personalized shopping experiences
- KR: increase CTR by 2% by tuning algo / 5% by adding more data sources / 10% by deep learning and even more data.


## 6- Career ladder

What leads to a raise or promotion?
Provide both individual-contributor and management tracks, going from junior to senior and principal.

Requirements fall in 3 categories:
- technical: ideally T-shaped skillset (be good overall, excellent in one thing).
- organizational: communicate effectively with peers and manager > mentor and develop ideas with PMs.
- personal: ask for help to unblock yourself, manage your time > can self-unblock, bring external innovation to the team > company-wide ownership mentality.

The report gives a full leveling guide.
