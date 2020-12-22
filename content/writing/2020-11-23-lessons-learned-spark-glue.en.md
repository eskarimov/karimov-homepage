+++
title = "Some lessons learned working with Spark/AWS Glue"
date = 2020-11-23
thumbnailPath = "self/img/thumbs/i-spark.png"
tags = ["spark", "engineering"]
isPopular = false
+++
Random general and specific notes from Notion made after a couple of projects
working with Spark/[AWS Glue](https://aws.amazon.com/glue/): 
- Parquet format doesn't support empty arrays
- Schema evolution in Spark 2.4 for ORC format [is broken]((https://issues.apache.org/jira/browse/SPARK-27913))
- Looking forward for [ZSTD compression for ORC format.](https://issues.apache.org/jira/browse/SPARK-33295)
- Always check that desired features work as expected - apparently dynamic partitioning pruning
doesn't work in AWS Glue as expected with broadcast join, reading the whole dataset on the left side.
  Hopefully works as expected starting Spark 3.0 (#TODO - test it)
- Another #TODO - test Apache Hudi for incremental data processing.
- [Great article about data repartitioning in Spark](https://medium.com/airbnb-engineering/on-spark-hive-and-small-files-an-in-depth-look-at-spark-partitioning-strategies-a9a364f908)