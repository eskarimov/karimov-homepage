+++
title = "Некоторые заметки после плотной работы с Spark/AWS Glue"
date = 2020-11-23
thumbnailPath = "/self/img/thumbs/i-spark.png"
tags = ["spark", "engineering"]
isPopular = false
+++

Случайные и не очень заметки из Ноушн после парочки проектов на Spark и [AWS Glue](https://aws.amazon.com/glue/):
- Parquet не поддерживает пустые массивы.
- Эволюция схемы [поломана в Spark 2.4 для ORC формата.](https://issues.apache.org/jira/browse/SPARK-27913)
- Очень жду поддержку [ZSTD компрессию для ORC формата в Спарке.](https://issues.apache.org/jira/browse/SPARK-33295)
- Всегда проверяй, что разные фишки работают, как ожидаешь - например, динамическое
партиционирование внезапно не работает в случае broadcast join'ов на AWS Glue, а читает весь
  датасет с левой части. (нужно проверить, как обстоят дела в Spark 3.0 - завезли много связанных с этим новых фишек)
- Apache Hudi - выглядит классно для инкрементальных загрузок данных, нужно потестить.
- [Отличная статья по репартиционированию данных в Спарке.](https://medium.com/airbnb-engineering/on-spark-hive-and-small-files-an-in-depth-look-at-spark-partitioning-strategies-a9a364f908)