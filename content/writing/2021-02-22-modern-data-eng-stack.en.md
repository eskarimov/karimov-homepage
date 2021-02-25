+++
title = "About the modern data engineering stack"
date = 2021-02-22
thumbnailPath = "/self/img/thumbs/laptop-hacker-code.jpg"
tags = ["data engineering", "big data"]
isPopular = false
+++

Not a secret we're living in the rapidly changing world, generating more and more machine data.
A new era of big data and so on, words you've probably heard hundreds of times already.
A lot of new and old companies want to get insights out of their data. Become data-driven is a new trend and motto.
Naturally many new, open-source tools and projects appeared against this background.

How can they help in democratising data landscape and how does the choice between commercial products/services
and open-source/in-house solutions look like in these circumstances?

I won't give a definitive answer, but rather share my thoughts.

Every case is pretty unique, although every company can experience similar issues/need of similar instruments.

Almost every single job description contains some of these keywords: Airflow, Python/SQL, Redshift/Snowflake/BigQuery, Tableau/Looker.

While it's totally understandable why the latter two are in this list, 
I'm often curious if it's absolutely necessary to write and maintain a bunch of operators/dags/hooks for Airflow?

Please get me right, I truly love Airflow, it's a super nice tool,
but still - can data engineers concentrate on more interesting tasks, rather than writing another connector to another source API?
In this light the modern instruments like [Fivetran](https://fivetran.com/)/[dbt](https://www.getdbt.com/) look quite interesting.

So here we come to touch the topic of when it makes sense to have a team of data engineers, 
maintaining all the DAGs/pipes copying data from sources and custom operators/logic.
It makes sense in the following cases:

- Amount of sources are low, and they aren't frequently added/changed
- Special security concerns
- Specific data sources, which aren't supported by cloud pipelines.

Every other use-case will potentially win by using [Stitch](https://www.stitchdata.com/)/Fivetran/etc - simply because it'd be more reliable solution.

Anyways it's still possible to combine the best from both worlds and use as Airflow tasks, as one of cloud pipelines to ingest the data.
Also there shouldn't be any fear regarding the data engineer's role - no one takes the job position away, but making it easier. 
I personally don't want to make myself an important employee, just because I know how a complex piece of some data fetcher's code works.

In the same time, there's another important factor - team's professional level.
I'd agree, that teams having it strong, would potentially benefit more by using their own solutions. 
Simply because it'd be enough flexible and tuned exactly to fit the company needs.
Quite often such teams also contribute back to the open-source community.

This is especially actual in the light of the modern data teams concepts - like [Data Mesh](https://martinfowler.com/articles/data-monolith-to-mesh.html),
when the bottle-neck layer of data engineers, responsible for every single data load, 
is pushed back to business-teams using this data, 
and ideally creating and maintaining ingestion pipelines with the help of data engineers, who support self-service data platform.

Thank you so much if you read the article all the way here.
I’d love to hear about your opinion and experiences.