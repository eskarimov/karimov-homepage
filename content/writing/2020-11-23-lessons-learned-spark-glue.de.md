+++
title = "Was ich gelernt habe bei der Arbeit mit Spark/AWS Glue"
date = 2020-11-23
thumbnailPath = "self/img/thumbs/i-spark.png"
tags = ["spark", "engineering"]
isPopular = false
+++
Zufällige allgemeine und spezifische Notizen aus Notion, 
die nach einigen Projekten mit Spark/[AWS Glue](https://aws.amazon.com/glue/) erstellt wurden:
- Das Parquet-Format unterschtützt keine leeren Arrays.
- Die Entwicklung eines Schemas in Spark 2.4 für das ORC-Format [funktioniert nicht.](https://issues.apache.org/jira/browse/SPARK-27913)
- ZSTD-Kompression für das ORC-Format [ist sehr erwartet.](https://issues.apache.org/jira/browse/SPARK-33295)
- Überprüf immer, ob die gewüncshten Fuktionen wie erwartet fuktionieren. Zum Beispiel 
  funktioniert dynamischen Partitionierung in AWS Glue mit Broadcast-Join nicht, sondern liest es
  den gesamten Datensatz von der linken Seite. Hoffentlich wird es ab Spark 3.0 behoben. (#TODO test's)
- Ein weiterer #TODO - test Apache Hudi für inkrementelle Datenverarbeitung in Spark.
- [Ein Großartiger Artikel über die Daten-Partitionierung in Spark.](https://medium.com/airbnb-engineering/on-spark-hive-and-small-files-an-in-depth-look-at-spark-partitioning-strategies-a9a364f908)
