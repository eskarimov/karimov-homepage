+++
title = "Notes about data catalog solutions"
date = 2021-01-25
thumbnailPath = "/self/img/thumbs/catalog.jpg"
tags = ["data catalog", "big data"]
isPopular = false
+++

Data catalogs have become an essential part of the modern data infrastructure and management.
It allows to have an overview of data, presented in the organisation, by storing metadata about it - such as location,
format, columns/attributes, etc.
This is especially important combined with the modern data teams architectures, such as [Data Mesh](https://martinfowler.com/articles/data-monolith-to-mesh.html), 
when every team can contribute to data catalog.

There's a growing interest in the industry to improve productivity of data engineers and scientists with metadata.
Following projects were released over the past several years:
- [Dataportal by AirBnb](https://medium.com/airbnb-engineering/democratizing-data-at-airbnb-852d76c51770)
- [Databook by Uber](https://eng.uber.com/databook/)
- [Amundsen by Lyft](https://www.amundsen.io/)
- [Metacat by Netflix](https://netflixtechblog.com/metacat-making-big-data-discoverable-and-meaningful-at-netflix-56fb36a53520)

Naturally a few startups appeared in this area as well, my favorite is [Tree Schema](https://treeschema.com/).

So far I've tried to use only [Amundsen together with Apache Atlas for tracking data lineage](https://medium.com/wbaa/facilitating-data-discovery-with-apache-atlas-and-amundsen-631baa287c8b), this is a great couple, 
however, another part, which is lacking in almost every product - a possibility to set and track data quality,
which I would like to touch in another article. 