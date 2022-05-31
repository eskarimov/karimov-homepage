+++
date = 2022-05-31
isPopular = false
tags = ["data engineering", "gcp", "google cloud"]
thumbnailPath = "/self/img/thumbs/laptop-tech.jpg"
title = "Takeouts on new GCP products DataPlex and Analytics Hub"

+++

Google has recently introduced new products [DataPlex](https://cloud.google.com/blog/products/data-analytics/build-a-data-mesh-on-google-cloud-with-dataplex-now-generally-available) 
and [Analytics Hub](https://cloud.google.com/blog/products/data-analytics/analytics-hub-data-exchange-now-in-public-preview) aiming to help engineers in building a modern data engineering stack.
With this writing, I'd like to share my first impressions working with them.

Let's start with DataPlex first.

Google promotes it as a data fabric, helping to unify distributed data and automate data management by building a domain-oriented data mesh.

The idea seems to be very nice, data might be stored in multiple GCP projects and Dataplex will govern and manage it without any data movement.

Let's dive deeper and see how it's implemented.

First, we need to create a new lake. Additionally, we can specify if we want to enable Hive Metastore service useful for querying data with instruments such as Presto, Hive, Spark.

![](/self/img/2022-05-31-new-gcp-products/create_new_lake.jpg)

On the next step we should get familiar with a concept of zones inside our lake.
A zone is a logical group of structured or unstructured data, such as GCS buckets and/or BQ datasets and tables.

There are 2 zones types available: raw and curated. Raw stores data in any format in GCS or BQ datasets. A curated zone stores structured data in GCS or BQ in certain formats such as Parquet, Avro or ORC.

So let's see how it works and create one raw and one curated zone.

![](/self/img/2022-05-31-new-gcp-products/create_zones.jpg)
This will accordingly create 2 datasets in BigQuery: analytics_raw, analytics_curated.

And now we come to the point where I personally get confused about Dataplex's concept.
I assumed that adding a new table to these datasets will make this table visible in Dataplex "Discover" or "Explore" tab.
However, when I added a new table to the raw dataset, nothing has appeared here.

![](/self/img/2022-05-31-new-gcp-products/example_table_analytics_raw.jpg)
A new table is added to the `analytics_raw` dataset.

![](/self/img/2022-05-31-new-gcp-products/analytics_raw_assets.jpg)
However, no assets are shown under `analytics-raw` and nothing is displayed in catalog either.

I could go even further and delete the dataset completely from BQ, and it won't affect the zone in Dataplex anyhow. So, I'm not sure what's the right relation between a zone in Dataplex and an according dataset in BQ.

Let's move on and try adding an asset to our zones.  
Assets help to map data stored in GCS or BQ into a single zone within a lake.

Here I'm adding a dataset `marts` containing a table `currency_rates` into the curated zone.
And here, suddenly, I can explore and find this dataset and table within "Explore" tab in Dataplex.

It's a mystery to me why the same doesn't work with datasets created per each zone.

![](/self/img/2022-05-31-new-gcp-products/curated_zone_asset.jpg)

Let's stop here for reviewing Analytics Hub and get back to Dataplex right after it, discussing which features from Analytics Hub might be very useful in Dataplex.

Analytics Hub is a platform for exchanging data across organization and external data providers.  
It is based on publish and subscribe model of BigQuery datasets.

In simple words, you can create a link to a dataset in another project inside yours, allowing to view and query it.  
Of course, it's not a big difference comparing it to regular grants to users, groups, service accounts or authorized views, however, having a linked dataset in your project makes is great for discovery and access control.

Here's how it works - there's a new tab in BQ menu, where you can find data exchanges and browse Analytics Hub datasets.

![](/self/img/2022-05-31-new-gcp-products/analytics_hub.jpg)

Important to mention, that you need to have enough a role Analytics Hub Viewer to a listing you're interested, in order to discover it in Analytics Hub catalog.  
After you've found an interesting dataset, you can "subscribe" to it, then a new linked dataset will appear within your project, which will be a read-mirror of the original dataset.

In my opinion it's a great improvement, however, it's lacking functionality to preview data (before having access to it) and requesting data owner to give you permissions.

What's missing to me overall is the information how to combine all the new products together - Dataplex, Analytics Hub, Data Catalog, plus now we have BigTable.
Google provides mainly marketing materials and videos, while in reality many questions or best practices left unanswered.

Hopefully these products will evolve together into a well-combined environment. Say, I'd really want to have an ability of managing access to multiple datasets within a single place, so that anyone within the company could preview the data and request access to it, and then a granted dataset would appear as a link in the requester's project.

Have you tried any of these new products or have any other thoughts? Please welcome to comments :) 
