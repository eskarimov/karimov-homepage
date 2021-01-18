+++
title = "Auswahl des Open-Source-Kommentarsystems"
date = 2021-01-11
thumbnailPath = "/self/img/thumbs/stickers.jpg"
tags = ["comments", "hugo"]
isPopular = false
+++

During this web-site development I naturally had an idea to add a comment system here.
Although [Hugo](https://gohugo.io/), which I use, supports Disqus out of the box, I'm not so happy about it due
to quite controversial opinions about it.

Während dieser Website-Entwicklung hatte ich natürlich die Idee, hier ein Kommentarsystem hinzuzufügen.
Obwohl [Hugo](https://gohugo.io/), den ich benutze, Disqus sofort unterstützt, bin ich nicht so glücklich darüber,
da es ziemlich kontroverse Meinungen dazu gibt.

Also fing ich an, nach Alternativen zu suchen und habe Commento ausgewält - es sieht ziemlich leicht aus
und einfach einzurichten.

Also habe ich alles eingerichtet, JS / HTML-Dinge hinzugefügt und wollte es 
genießen - aber anscheinend ist ein Problem aufgetreten, 
als ich versucht habe, Authentifizierungsanbietern, insbesondere Github, zu verbinden.
Nach einer kurzen Recherche wurde es festgestellt, dass
Github eine Antwortstruktur für Authentifizierungsanforderungen geändert hat
und [Commento diese noch nicht unterstützt](https://gitlab.com/commento/commento/-/issues/367). 
Nachdem ich Probleme im Gitlab-Tracker untersucht hatte, 
hatte ich das Gefühl, dass [das Projekt nicht mehr entwickelt wird]((https://gitlab.com/commento/commento/-/issues/377)).

Ok, dann suche ich nach einem anderen Projekt.

Einer der Kandidaten, die ich sofort in Betracht gezogen habe, 
war Remark42 - es war auch in meiner ersten Shortlist,
Aber ich war nicht sehr glücklich über das Design und fand Commento leichter.
Wichtige Kriterien bei mir sind:
- Unterstützung von OAuth-Anbietern, zumindest Google, Github, möglicherweise Twitter, idealerweise Telegramm.
- Markdown-Unterstützung für Kommentare
- Verschiedene Farbschemata
- Leichtgewicht, ohne Tracking-Skripte im Inneren
- Sei am Leben und bleibe in aktiver Entwicklung

Remark42 erfüllt mehr oder weniger alle Anforderungen und [verspricht derzeit sogar,
Telegramm zu unterstützen](https://github.com/umputun/remark42/issues/707).
Also habe ich mich dafür entschieden, das Setup 
war wirklich einfach - Sie können das Ergebnis unten im Kommentarbereich überprüfen.
Lassen Sie mich Ihre Gedanken wissen und zögern Sie nicht, Fragen zu stellen :)
