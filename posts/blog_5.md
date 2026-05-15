---
title: External Data, Internal Panic
date: 2026-05-09
author: Zhenghao Gu
summary: I explored how APIs could connect our project to external data, while also realising that every API-powered feature brings extra complexity, failure cases, and security concerns.
tags:
  - APIs
  - Database
  - Error Handling
---

At this point, our website is almost ***finished***.

This week, we refined the CSS and database, and experimented with integrating some APIs.

After finishing all the basic contents, I moved on to improving the CSS. This part was actually quite satisfying, because the website immediately looked more like a real product instead of a skeleton wearing no clothes. I focused on making the homepage, Sound Room cards, and detail page more consistent, especially spacing, layout, and visual hierarchy. The goal was not to make everything perfect, but to make the pages feel like they belonged to the same system.

At the same time, we also worked on the database. This directly Inherited from the DDD and ERD work from last week. Before, the Sound Room cards were basically fixed content written into HTML. Now, I started thinking about them as pieces of data that could eventually come from the database: title, description, creator, tags, comments, and other details. This made the project feel much more real, but also more stressful. Static HTML is obedient. Database logic is not always obedient.

We also started looking at APIs and external data. In the tutorial, the example was weather and geocoding, which is not directly related to our indie music website, but the logic was useful. The important idea was that a web app can ask another system for information, receive structured data, and then display it to users. For our project, this made me think about possible future features, such as music metadata, artist information, album covers, or event-related data.

However, I also realised that adding an API is not just adding a cool feature. It creates extra problems: what if the request fails, what if the data is missing, what if the API has limits, or what if the feature becomes too complicated for our current prototype? So the main trade-off this week was between making the website more interactive and keeping it manageable. I wanted the site to feel alive, but I also did not want to accidentally create a monster.

We also began adding small interactions. Nothing too dramatic yet, but enough to make the website feel less static. For example, users should be able to move from the homepage into a Sound Room, read or interact with comments, and understand that the page is responding to them. This made me realise that interaction is not only about animation or fancy effects. It is about giving users feedback and making the system feel understandable.

By the end of the week, the project felt much closer to a working prototype. The CSS made it more visually coherent, the database gave the content a clearer structure, the API work opened up new possibilities, and the interactions made the website feel less frozen. There is still a lot to fix, of course.

There is always a lot to fix.

I’ve got a bunch of deadlines coming up, and I feel like I’m going to be ***"dead"***.