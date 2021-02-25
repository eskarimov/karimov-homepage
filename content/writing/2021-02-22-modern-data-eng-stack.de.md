+++
title = "Zum modernen Data Engineering Stack"
date = 2021-02-22
thumbnailPath = "/self/img/thumbs/laptop-hacker-code.jpg"
tags = ["data engineering", "big data"]
isPopular = false
+++

Es ist kein Geheimnis, dass wir in einer sich schnell verändernden Welt leben und immer mehr Maschinendaten generieren. 
Eine neue Ära von Big Data und weitere Wörter, die Sie hunderte Male gehört haben. 
Viele neue und alte Unternehmens möchten Einblicke auf ihre Daten erhalten. 
Sei Data-Driven ist ein neuer Trend und ein neues Motto. 
Vor diesem Hintergrund erschienen natürlich viele neue Open-Source-Tools und Projekte.

Wie können sie bei der Demokratisierung der Datenlandschaft helfen und
wie sieht die Wahl zwischen kommerziellen Produkten / Dienstleistungen und Open-Source- / Inhouse-Lösungen unter diesen Umständen aus?

Ich gebe keine endgültige Antwort, sondern meine Gedanken teilen.

Und zuerst muss ich sagen, dass jeder Fall ziemlich einzigartig ist, obwohl jedes Unternehmen ähnliche Probleme und Bedürfnisse haben kann.

Also fast jede Stellenbeschreibung für einen Data Ingenieur enthält einige von diesen Schlüsselwörtern: Airflow, Python, SQL, Redshift/Snowflake/Bigquery, Tableau/Looker.

Obwohl es komplett verständlich ist, warum die beiden letzteren in dieser Liste sind, bin ich neugierig, 
ob es absolut notwendig ist, eine Reihe von Operatoren/DAGs/Hooks für Airflow zu erschaffen und unterstützen.

Bitte verstehen Sie mich richtig, ich mag Airflow, es ist ein sehr praktisches Tool, 
aber trotzdem - können Dateningenieure sich auf interessantere Aufgaben konzentrieren gönnen, anstatt einen anderen Connector für eine andere API-Quelle zu schreiben?

Hier kommen wir also zum Thema, wann es sinnvoll ist, ein Team von Dateningenieuren, das alles DAGs, Prozesse verwaltet,
zu haben. Meine Meinung nach ist es in folgenden Fällen sinnvoll:

- Die Anzahl der Quellen ist gering und sie sind nicht häufig hinzugefügt oder geändert
- Besondere Sicherheitsbedenken
- Spezifische Datenquellen, die von Cloud-Pipelines nicht unterstütz werden.

Jeder andere Anwendungsfall wird möglicherweise durch die Verwendung von [Stitch](https://www.stitchdata.com/) / [Fivetran](https://fivetran.com/) oder ähnliches gewinnen - einfach,
weil dies eine zuverlässigere Lösung wäre.

Gleichzeitich ist es immer noch möglich, 
das Beste aus beiden Welten zu kombinieren und sowie Airflow, als auch Cloud-pipelines zu haben.

Es ist wichtig zu betonen, dass man keine Angst vor der Rolle des Dateningenieurs in diesem Fall haben soll. 
Denn niemand nimmt die Stelle weg, sondern macht es die Arbeit einfacher und effektiver. 
Ich persönlich würde mich nicht zu einem wichtigen Mitarbeiter machen, nur weil ich weiß, 
wie ein komplexer Teil des Codes funktioniert.

Es gibt noch einen wichtigen Faktor in diesem Bereich - die Professionalität des Teams. 
Und hier würde ich zustimmen, dass Teams, die es stark haben, mehr davon profitieren würden, 
wenn sie ihre eigenen Lösungen verwenden. Einfach,
weil sie genug flexibel und genau auf die Anforderungen des Unternehmens abgestimmt wären. O
ft tragen solche Teams auch zur Open-Source- Community bei.

Dies gilt insbesondere im Hinblick auf die modernen Konzepte von Datenteams - wie [Data Mesh](https://martinfowler.com/articles/data-monolith-to-mesh.html), 
wenn die Flaschenhalsschicht von Dateningenieuren, die für jede einzelne Datenladung zuverlässig sind, an jedes Team, 
das die Daten benutzt, zurückgeschoben wird. 
Und jedes Team erstellt Datenladen selbst, aber mithilfe von Dateningenieuren, 
die eine Self-Service-Datenplattform unterstützen.

Vielen Dank, wenn Sie den Artikel gelesen haben. 
Ich würde gern von Ihrer Meinung und Ihren Erfahrungen hören.