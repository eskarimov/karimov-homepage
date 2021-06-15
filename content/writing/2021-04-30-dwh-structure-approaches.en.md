+++
title = "DWH approaches"
date = 2021-06-15
thumbnailPath = "/self/img/thumbs/stats-monitor.jpg"
tags = ["data engineering", "big data"]
isPopular = false
+++
With this post I'd like to cover some well-know approaches to data-warehousing in order to have a brief overview of them: 
- [Inmon](#Inmon)
- [Kimball](#Kimball)
- [Data Vault](#Data Vault)
- [Data Lake](#Data Lake)
- [Lakehouse](#Lakehouse)

I'm not aiming to cover all the details of each approach in this article, as each of them deserves its own separate article.

### Inmon 
Let's start first with the methodology created by Bill Inmon, which is considered to be a top-down approach.
This methodology assumes that the structure of the data is known from top to down, there's a whole picture of it availble
 and data is modelled accordingly to the 3NF (Normal form).
Each logical model contains all the details related to that entity. The key point is that data stored in the normalized form.
Data redundancy is avoided as much as possible.
The biggest downside of this approach is that the data should be described from top to down, what required very skillful people
to design it and keep integration between all the components, which might be complicated in the enterprise-level companies.

### Kimball
In opposite to the Inmon approach this one by Ralph Kimball is considered to be a bottom-up approach.
Key sources (operational systems) are identified and documented.
ETL tools bring data from different sources and load it into the staging area.
Then data is loaded into the dimensional tables. The key point is that the data isn't normalized as data is organized 
either in Star or Snowflake (under certain circumstances) schema.

### Data Vault
The DV model, in a nutshell, is a layer that exists between regular dimensional modeling (OLAP, Star Schema) and 
Staging that provides scaling with growing business requirements and serves to break down complexities of both the modeling and ETL.
It’s composed of hubs (business entities), links (relationships) and satellites (descriptive attributes)
It's especially useful, when a good support of tracking historical changes is required, as it stores all the facts,
without distinction to good and bad data, is opposite to other DWH methods of storing "a single version of truth".

The modeling method is designed to be resilient to change in the business environment
where the data being stored is coming from, by explicitly separating structural information from descriptive attributes.
Data vault is designed to enable parallel loading as much as possible, so that very large implementations can
scale out without the need for major redesign.

### Data lake
A very popular approach nowadays, as amount of data grows significantly and introduces silos between different departments,
especially in big enterprise companies.
Opposite to the traditional DWH approaches, Data Lake stores all the information from source systems as-is (i.e. raw data),
optionally some auditing columns to show where the data came from, when it was loaded, etc.
Important to mention it's not just data is use today, but also data that may be used and even data that may never be used just
because it might be used someday.
Hence, commodity, off-the-shelf servers combined with cheap storage makes scaling a data lake to terabytes and petabytes fairly reasonable.
It's like a giant tub of assorted Lego bricks and no defined plan as to how to put it together,
and some of the bricks will be non-standard – it’s up to the person playing with the bricks to assemble it how they see fit to meet their needs.

Some data lakes have multiple layers e.g. the raw data layer and then a governed data layer where the data has been cleansed, 
standardised, etc. - but is still in basically the same structure as in the raw data layer.

### Lakehouse
This approach tends to take the best from both worlds: Data Warehouse and Data Lake, providing a single platform
for all data transformations, business intelligence and data science.
Storage and compute levels are separated, implementing similar data structures and data managements features to those in a data darehouse,
directly on the kind of low-cost storage used for data lakes.
The approach assumes the following advantages:
- Data governance may be simplified with a single control point
- Keep data in the same data lake format
- Schema management is simplified
- Transaction support with ACID compliance