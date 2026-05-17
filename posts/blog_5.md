---
title: External Data, Internal Panic
date: 2026-05-09
author: Zhenghao Gu
summary: I polished project's CSS, linked database, and explored how APIs could connect our project to external data.
tags:
  - CSS
  - Database
  - APIs
---

At this point, our website is almost ***finished***.

This week, we refined the CSS and database, and experimented with integrating some APIs.

After finishing all the basic contents, I moved on to improving the CSS. This part was actually quite satisfying, because the website immediately looked more like a real product instead of a skeleton wearing no clothes. I focused on making the homepage, Sound Room cards, and detail page more consistent, especially spacing, layout, and visual hierarchy. The goal was not to make everything perfect, but to make the pages feel like they belonged to the same system.

At the same time, we worked on the database. This directly Inherited from the DDD and ERD work from last week. Before, the Sound Room cards were basically fixed content written into HTML. Now, I started thinking about them as pieces of data that could eventually come from the database: title, description, creator, tags, comments, and other details. This made the project feel much more real, but also more stressful. Static HTML is obedient. Database logic is not always obedient.

This also made me think about responsibility beyond whether the prototype works. I often see cookie notices on websites, and I think developers do a great job of it. Because our website involves user profiles, comments, and possibly music-related preferences, it may handle personal or community-sensitive information. This means we should avoid collecting unnecessary data, clearly explain what information is stored, handled properly. If the project became a real product, the respectful data management would not be optional extras. They would be part of whether the system is actually acceptable to use.

We also started looking at APIs. In the tutorial, the example was weather and geocoding, which is not directly related to our indie music website, but the logic was useful. Choosing an API is not as simple as finding one that “does the function”. There are many APIs that look similar on the surface, but they are not exactly the same in practice. Some provide richer data but have stricter limits, some are faster but return less useful information, and some require API keys or more complicated setup, which are significant trade-offs.

After all, the important idea remains that a website can ask another system for information, receive structured data, and then display it to users. For our project, this made me think about possible future features, such as recommendation based on the location, artist information, album covers, or events' live data.

We also began considering and adding interactions. For example, users should be able to move from the homepage into a Sound Room, read or like a comment, and understand that the page is responding to them. I originally had quite a few creative ideas for animations that I thought were “really smart,” but after trying them out, I realized that many were actually beyond our capabilities. In the end, I decided that simple, smooth animations could achieve a similar effect.

***What matters isn’t the animation itself, but how users perceive the system’s feedback.***

By the end of the week, the project felt much closer to a working website. The CSS made it more visually coherent, the database gave the content a clearer structure, the API work opened up new possibilities, and the interactions made the website feel more powerful. There is still a lot to fix, of course.

There is ***always*** a lot to fix.

I’ve got a bunch of deadlines coming up, and I feel like I’m going to be ***"dead"***.