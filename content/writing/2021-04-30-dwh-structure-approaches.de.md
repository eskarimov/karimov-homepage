+++
title = "DWH Konzepte"
date = 2021-06-15
thumbnailPath = "/self/img/thumbs/stats-monitor.jpg"
tags = ["data engineering", "big data"]
isPopular = false
+++
In diesem Artikel möchte ich einige bekannte Data Warehousing Konzepte behandeln, um einen kurzen Überblick darüber zu bauen:
- [Inmon](#Inmon)
- [Kimball](#Kimball)
- [Data Vault](#Data-Vault)
- [Data Lake](#Data-Lake)
- [Lakehouse](#Lakehouse)

Ich habe kein Ziel, alle Kleinigkeiten jedes Konzeptes hier zu außern, weil jedes Konzepz einen eigenen Artikeln verdient.

### Inmon
Beginnen wir zunächst mit der von Bill Inmon entwickelten Methodik, die als Top-Down-Ansatz gilt.
Diese Methodik geht davon aus, dass die Struktur der Daten von oben nach unten bekannt ist, es gibt ein Gesamtbild davon
und Daten werden entsprechend der 3NF (Normalform) modelliert.

Jedes logische Modell enthält alle Details zu dieser Entität. Der wichtigste Punkt ist, dass die Daten in der normalisierten Form gespeichert werden.
Datenredundanz wird weitestgehend vermieden.
Der größte Nachteil dieses Ansatzes ist, dass die Daten von oben nach unten beschrieben werden sollten.
Dafür sind sehr erfahrene Leute erforderlich, um dieses System zu entwerfen und die Integration zwischen allen Komponenten aufrechtzuerhalten.
Das gilt besonders stark für große Unternehmen.

### Kimball
Im Gegensatz zum Inmon-Ansatz gilt dieser von Ralph Kimball als Von-unten-nach-oben-Ansatz.
Hauptquellen (operative Systeme) werden identifiziert und dokumentiert.  
Normalerweise ist es einfacher, mit Kimball zu beginnen, die Daten nach Abteilungen in Data Marts aufzuteilen.
Aber es wird später schwieriger, das Model zu skalieren.  
ETL-Tools bringen Daten aus verschiedenen Quellen und laden sie in den Staging-Bereich.
Anschließend werden die Daten in die Dimensionstabellen geladen. Der entscheidende Punkt ist, dass die Daten nicht normalisiert werden,
weil die Daten entweder im Star- oder Snowflake-Schema (unter bestimmten Umständen) organisiert werden.

### Data Vault
Das DV-Modell ist kurz gesagt eine Schicht, die zwischen der regulären dimensionalen Modellierung (OLAP, Star Schema) 
und dem Staging existiert, die eine Skalierung mit wachsenden Geschäftsanforderungen ermöglicht und dazu dient, 
die Komplexität sowohl der Modellierung als auch der ETL aufzuschlüsseln.
Es besteht aus Hubs (Geschäftseinheiten), Links (Beziehungen) und Satelliten (beschreibende Attribute)
Es ist besonders nützlich, wenn eine gute Unterstützung bei der Verfolgung historischer Änderungen erforderlich ist, 
da alle Fakten speichert wedrden, ohne Unterschied zwischen guten und schlechten Daten.

Die Modellierungsmethode ist so konzipiert, dass sie gegenüber Veränderungen im Geschäftsumfeld widerstandsfähig ist, 
weil strukturelle Informationen explizit von beschreibenden Attributen getrennt werden.
Data Vault ist so konzipiert, dass er so viel wie möglich paralleles Laden ermöglicht, sodass es möglich ist,
sogar sehr große Implementierungen ohne große Neugestaltung zu skalieren.

### Data lake
Ein heutzutage sehr beliebter Ansatz, da die Datenmenge viel aufwachsen sind und Silos zwischen verschiedenen Abteilungen einführt,
vor allem in großen Konzernen.
Im Gegensatz zu den traditionellen DWH-Ansätzen speichert Data Lake alle Informationen aus Quellsystemen unverändert (d. h. Rohdaten),
optional auch einige Audit-spalten, um anzuzeigen, woher die Daten kamen, wann sie geladen wurden usw.
Es ist wichtig zu erwähnen, dass es nicht nur um die Daten geht, die heute verwendet werden, sondern auch um Daten,
die möglicherweise verwendet werden und sogar um Daten, die möglicherweise nie verwendet werden,
nur weil sie eines Tages verwendet werden könnten.
Daher machen handelsübliche Standardserver in Kombination mit billigem Speicher die Skalierung eines Data Lake 
auf Terabyte und Petabyte ziemlich vernünftig.
Es ist wie eine riesige Kübel mit verschiedenen Legosteinen und es gibt keinen definierten Plan, wie man es zusammenbaut.
und einige der Steine können nicht standardmäßig sein – es liegt an der Person, die mit den Steinen spielt, 
sie so zusammenzusetzen, wie sie es für richtig hält, um ihre Bedürfnisse zu erfüllen.

Einige Data Lakes haben mehrere Schichten, z.B. die Rohdatenschicht und dann eine geregelte Datenschicht, in der die Daten bereinigt wurden,
standardisiert, etc. - aber im Grunde immer noch in der gleichen Struktur wie in der Rohdatenschicht.

### Lakehouse
Dieser Ansatz versucht das Beste aus beiden Welten zu benutzen: Data Warehouse und Data Lake, und die eine einzige Plattform
für alle Datentransformationen, Business Intelligence und Data Science anzubieten.
Speicher- und Rechenebene sind getrennt und implementieren ähnliche Datenstrukturen und Datenverwaltungsfunktionen wie in einem Datawarehouse.
direkt auf die Art des kostengünstigen Speichers, der für Data Lakes verwendet wird.
Der Ansatz geht von folgenden Vorteilen aus:
- Data Governance kann mit einem einzigen Kontrollpunkt vereinfacht werden
- Daten im gleichen Format sind gespeichert 
- Schemaverwaltung wird vereinfacht
- AKID Transaktionsunterstützung 
