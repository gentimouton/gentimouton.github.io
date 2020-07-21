---
layout: post
title: Setting up analytics and BI tools
excerpt_separator: <!--more-->
---

Notes from a [Holistics.io book](https://www.holistics.io/books/setup-analytics/) on setting up analytics and BI tools.

<!--more-->


# Chapter 1. High-level Overview of an Analytics Setup

Basics: dirty (ie raw operational) data in lake > clean data in data warehouse (DW) > visualization/reporting/ML to stakeholders.

Holistics' tenets:
- ELT rather than ETL
- DW in cloud rather than on premise
- center on data modeling
- analytics: SQL rather than not SQL
- focus on analytics workflow rather than visualization

# Chapter 2. Centralizing Data

DW is where you store and process data for analytics.

ETL: data transformed in the tool's memory, then dumped into DW.
Comapre to ELT: data transformed within the DW.
Now that storage is cheap, ELT is better than ETL.

Extract and Load is much more than just an `select * from source_db`. 
So don't reinvent the wheel, and use off-the-shelf ETL tools:
- ETL tools: Airflow, Prefect, Meltano, Talend, Stitchdata.
- DW: Redshift, Bigquery, Snowflake, Presto.
- Data lake: S3 or GCS.
- Transform tools (to clean, aggregate, pre-compute): dbt, Looker, Holistics.

# Chapter 3. Data Modeling for Analytics

Data Analyst implements business logic into data logic in the modeling layer, eg via dbt.
This enables self-serve analytics for stakeholders.
Goal of modeling is self-service, so business needs/usage determine modeling, not the other way.

Data models are abstract, unlike tables.
Models store metadata too, via calculated/derived fields, and relationship mapping.
Models can be persisted back into DW.

Modeling approaches: Kimball, Inmon, Data Vault, star schema.

Modeling has 4 steps: pick business process, decide grain, choose dimensions, choose measures.

For slow-changing dimensions, snapshot them all daily, because storage and compute is cheap, but engineer's time is expensive.

# Chapter 4. Using Data

1990s: Mostly banks shuffled data, and 1GB RAM cost $30k. Analysts used Cognos to see available cubes made by data engineers. 
Waterfall process meant updating cubes took weeks. Bootlenecked on data engineers.

2000s: Tech companies appear. Analysts use SQL Server for DW, and to define and run cubes. 
Any employee can go to Tableau and self-service their metric. 
Problem: every team defines metrics their own way in Tableau, leading to discrepancies and confusion.

2016: Tech startups. Analysts define metrics in a single place in Looker, which runs ELT on top of Redshift DW. 

No-SQL tech from early 2010s like Hadoop or Spark did not catch up for analytics compared to SQL, because analysts are not engineers, and only know SQL.

| Dimension of BI tool | Old way | Recommended by Holitsitcs |
|---|---|---|
| SQL vs Non-SQL | Non-SQL: Tableau, PowerBI, Sisense | SQL: Holistics, Looker, Mode, Redash, Metabase |
| Embedded Datastore vs External Datastore | Embedded: MicroStrategy, Tableau, PowerBI, Sisense | External: Holistics, Looker, Metabase, Redash |
| In-memory (ie local) vs In-database | In-memory: Tableau, MicroStrategy, Sisense, PowerBI, etc. | In-database: Holistics, Looker, Redash, Metabase, etc. |
| Modeling vs non-modeling BI tools | Non-modeling: Tableau, Mode, Redash | Modeling: Qlik, PowerBI, Looker, Holistics |

Company data maturity cycle: first ad-hoc queries, then static reports/dashboards, then self-service from prepared datasets.
