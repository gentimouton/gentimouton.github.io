---
layout: post
title: The care and feeding of data scientists
excerpt_separator: <!--more-->
---

This post is my notes on a [white paper](https://oreilly-ds-report.s3.amazonaws.com/Care_and_Feeding_of_Data_Scientists.pdf)
by [Michelangelo D'Agostino](https://www.linkedin.com/in/michelangelod/)
and [Katie Malone](https://www.linkedin.com/in/caitlin-malone-46050854/) on managing data scientists.
Overall, the report is a good introduction to the basics of managing DS, and provides a few generally-applicable guidelines.
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

