+++
title = "Choosing open-source comment system"
date = 2021-01-11
thumbnailPath = "/self/img/thumbs/stickers.jpg"
tags = ["comments", "hugo"]
isPopular = false
+++

During this web-site development I naturally had an idea to add a comment system here.
Although [Hugo](https://gohugo.io/), which I use, supports Disqus out of the box, I'm not so happy about it due 
to quite controversial opinions about it.

So I started to search for alternatives and stopped on Commento - it looks quite lightweight
and easy to setup.  

So I set all up, added JS/HTML things, and wanted to enjoy - but an issue is apparently 
appeared when I tried to connect 3-rd party auth providers, particularly Github.  
After a short research it was found that Github has changed a response structure for auth requests,
and [Commento doesn't yet support it](https://gitlab.com/commento/commento/-/issues/367) and after 
exploring issues in the Gitlab tracker I had a feeling that [the project isn't being developed anymore](https://gitlab.com/commento/commento/-/issues/377).  

Ok, lessons learned - let's look for another project.

One of the candidates I immediately considered was Remark42 - it was also in my first shortlist,
but I wasn't very happy about its design, finding Commento more lightweight.  
Important criteria are:
- support OAuth providers, at least Google, Github, maybe Twitter, ideally Telegram.
- Markdown support for comments
- Different color schemas
- Lightweight, without tracking scripts inside
- Be alive and stay under active development

Remark42 meets all the requirements more or less, and [currently even promises to support Telegram](https://github.com/umputun/remark42/issues/707).
So I decided to go for it, the setup was really easy - you can check the result below in the comments section.  
Let me know your thoughts and feel free to ask any question :)