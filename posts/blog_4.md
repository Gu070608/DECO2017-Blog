---
title: "DDD", DND?
date: 2026-05-02
author: Zhenghao Gu
summary: I struggled with moving from static HTML to data thinking, using DDDs and ERDs to understand how elements should connect behind the interface.
tags:
  - Annotated Wireflow
  - DDD & ERD
  - Clearer HTML
---

I think this week's material is giving me the most trouble.

This week's content focuses more on building the website's structure rather than the part that users see.

After working on the basic HTML last week, I realised that the pages could not just exist as static layouts forever. The Sound Room cards, user profile, comments, and discussion areas all look simple on the screen, but they actually need data behind them.

***A card is not just a card.***

It needs a title, description, image, creator, tags, created date, and probably a link to its detail page. Very suddenly, every small box on the page became ***suspicious***.

During our tutorial this week, we annotated our wireflow, marking the visible content, user inputs, and elements that would need data behind them. Then, our group started building the DDD and ERD for the project.

At first, I thought this would be a very technical step, almost like something that only belongs to CS people. But when we started writing the DDD, it felt more like translating the website into a clearer language. For each important thing on the page, we had to ask: what is this thing, what information does it need, and what would a real example look like?

For instance, for our features in each Sound Room, the main entities became clearer. We need users, Sound Rooms, comments, and tags or categories. The Sound Room is the centre of the experience, but it cannot exist alone. It is created by a user, displayed on the homepage, opened on the detail page, and connected to comments or bullet comments. This helped me understand that the homepage and detail page are not separate pieces. They are different views of the same data.

The DDD helped me improve the HTML as well. Some parts of my previous HTML were still based on what looked nice in the wireframe, not what the system actually needed. For example, the repeated Sound Room cards made me think about the HTML as a reusable pattern, obviously. Each card should follow the same structure: a title, description, creator information, tags, and a link to the room detail page. This made the HTML easier to connect with the DDD later, because each visible element could be mapped back to a specific attribute instead of being treated as random content.

Then we moved from DDD to ERD, which was honestly a bit more ***confusing***. Writing attributes is one thing; deciding relationships is another thing. For example, one user can create many Sound Rooms, and one Sound Room can have many comments. That part makes sense. But tags are more annoying, because one Sound Room can have multiple tags, and one tag can belong to multiple rooms. This made me realise why some relationships need extra structure instead of just putting everything into one messy list.

The main trade-off was between keeping the data model simple and making it flexible enough for the website later. If we make the structure too simple, it may be easier to build now, but harder to expand. If we make it too complex, we might create a system that is technically impressive but painful to actually finish. So for now, we tried to focus on the core functions first: users can browse Sound Rooms, enter a room, listen, and interact through comments.

By the end of the week, I felt like my HTML had a clearer and more completed structure. It was no longer just “finish three pages.” It became more like: build pages that can eventually connect to real data.

Which is ***huge*** progress.