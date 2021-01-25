+++
title = "Notizen über Datenkataloglösungen"
date = 2021-01-25
thumbnailPath = "/self/img/thumbs/catalog.jpg"
tags = ["data catalog", "big data"]
isPopular = false
+++

Datenkataloge sind zu einem wesentlichen Bestandteil der modernen Dateninfrastruktur geworden.
Es ermöglicht einen Überblick über Organisationsdaten, 
indem Metadaten darüber gespeichert werden - wie z. B. Speicherort, Format, Attribute usw.
Dies ist besonders wichtig in Kombination mit den modernen Architekturen von Datenteams wie [Data Mesh](https://martinfowler.com/articles/data-monolith-to-mesh.html),
wenn jedes Team zum Datenkatalog beitragen kann.

In der Branche wächst das Interesse, die Produktivität von Dateningenieuren und Wissenschaftlern mit Metadaten
zu verbessern. Folgende Projekte wurden in den letzten Jahren veröffentlicht:
- [Dataportal von AirBnb](https://medium.com/airbnb-engineering/democratizing-data-at-airbnb-852d76c51770)
- [Databook von Uber](https://eng.uber.com/databook/)
- [Amundsen von Lyft](https://www.amundsen.io/)
- [Metacat von Netflix](https://netflixtechblog.com/metacat-making-big-data-discoverable-and-meaningful-at-netflix-56fb36a53520)

Natürlich sind auch in diesem Bereich einige Startups aufgetaucht, mein Favorit ist [Tree Schema](https://treeschema.com/).

Bisher habe ich ausprobiert, nur Amundsen zusammen mit Apache Atlas (zur Verfolgung der Datenherkunft) zu verwenden.
Dies ist jedoch ein großartiges Paar, ein weiterer Teil, der in fast jedem Produkt fehlt – eine Möglichkeit, 
die Datenqualität festzulegen und zu verfolgen. Darüber möchte ich in den weiteren Artikeln reden.