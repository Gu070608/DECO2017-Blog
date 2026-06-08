---
title: Final Reflection
date: 2026-06-06
author: Zhenghao Gu
summary:  The final reflection on the whole development of Shen_ren.indie.music.
tags:
  - DECO2017
  - Final
  - Refelction
---

## Evaluation of Performance and Technical Behaviour

Looking back at the development of **Shen_ren.indie.music**, I think that while we have a great-looking UI and solid content, the most critical aspects are still database development and the user experience. At the beginning, I mainly thought about pages and visual layout: homepage, Browse, Profile, Community, and About. However, as the project developed, I realised that the application could not work properly if each page was treated separately. So does the databse. The Sound Room system needed a shared data structure behind it, so the same room, tag, user, post, and comment data could appear across different parts of the site.

This is where the ERD became much more important than I expected. Before this project, I had not really built a web application where so many types of data were related to each other. In this prototype, `sound_rooms` are connected to `tags`, `members`, `posts`, and `comments`. Tags are also separated into categories such as genre, mood, and location, which means that filtering is a real database relationship. Posts belong to a specific sound room and a member, while comments belong to posts and members. These elements bring the entire website to life, because one room could be displayed on the homepage, filtered through Browse, opened through a detail page, and connected to comments without duplicating the same information in HTML.

However, testing also showed that database-driven design creates new kinds of problems. At one point, the interface displayed undefined values because the frontend JavaScript expected different field names from the database. The script was reading fields such as `name` or `online`, but the SQL query returned fields such as `title`, `member_count`, `comment_count`, and `cover_image`. The database was not broken, but the frontend and backend were not speaking the same language. In particular, the entire language is case-sensitive, so I need to plan out the names and logic of each tag in advance, rather than just writing them as they come to mind. So that performance is not only about whether the query runs quickly; it is also about whether the data returned by the backend can be used reliably by the interface. After fixing the field mapping, the same database records could be reused consistently across the homepage, Browse, and room detail pages.

Another example was the location detecting feature. I used an API of IP-stack so the homepage could recommend local rooms. During testing, the detected location was Waterloo, but the database did not have a `waterloo` location tag. It had `sydney`. As a result, the system returned no local rooms even though Sydney rooms existed in the database. This was a useful performance issue because the application did not crash, but it failed to give the user a useful result. I fixed this by normalising suburbs such as Waterloo, Redfern, Mascot, and Newtown into the broader `sydney` tag. Later, I also realised that the location tags in the database were not only real cities. They included tags such as `berlin`, `hong-kong`, `tokyo`, `new-york`, as well as more conceptual locations such as `bedroom`, `studio`, and `cafe`. Because of this, the API logic had to be adjusted to reflect the actual ERD and seed data rather than my first assumption that location only meant major cities. This made the system more reliable because finally the API response became aligned with the database structure.

Overall, the final prototype performed good enough for a class project, but the testing process showed that technical behaviour depends on the relationships between data, routes, templates, and JavaScript. The application was strongest when these layers were aligned. It struggled when one layer made assumptions that another layer did not support. If I had more time, I would evaluate performance more formally with Lighthouse and other test flows. I would also improve image optimisation, add lazy loading, and create clearer empty and loading states for API responses. These improvements would make the application not only faster, but also more predictable and reliable when users interact with it.

## Evaluation of User Experience and Accessibility

A user start from the homepage, explore the rotating room carousel, scroll through recommendation rows, click into a room detail page, or use “View all” links to open filtered Browse results. Then, they get interest with talking to other fans under the comments, clicking the Community page. At night, when users are tired from all-day work, they open Discover, and finally enter Profile to logout.

**What a day!**

The user experience of the final prototype changed a lot through testing and feedback.

When I was still sketching, I showed the early structure to my friend and received feedback that some parts of the platform were visually interesting but not immediately clear as a user flow. For example, the idea of “Sound Rooms” was strong, but the early design did not fully explain how a user would move from discovering a room to actually entering it. This helped me focus more on the journey between pages.

In the prototype stage, I tested the interface again and realised that Browse was one of the most important pages. Earlier, the tags felt confusing because they were mixed together without a clear structure. A user could see many tags, but it was not obvious whether a tag described a genre, a mood, or a location. I redesigned the filters into three separate categories: genre, mood, and location, so users could filter based on intention. I also made the homepage recommendation links pass real query parameters, so these became more logical and linked to the Browse page smoother.

> “There are many tags, and I cannot tell which one is what category, they are all messed up together.”

Another improvement from prototype testing was the Room Detail page. Before adding it, clicking “Enter Room” did not really feel like entering a room —— it mostly sent users back to browsing or searching. This made the core concept weaker, because the “room” existed only as a card. In the final version, each room has its own /rooms/:id page with a large rotating record image, room information, a player-style section, posts, comments, and a comment form. When designing this, I drew inspiration from music streaming apps like Spotify and QQ Music. It also supported the community goal more clearly because users can read room-related discussion and submit their own comment. However, this comment system isn't quite ready yet; for example, the “like” feature and nested comments haven't been implemented yet. I expect these features will be included in a future development.

> “Room details look a bit of boring, I expected more in visual design or diagrams or something.”

For accessibility, I used WAVE and AIM scores as evidence to evaluate. This helped me identify issues that were not obvious from visual inspection alone. For example, the homepage originally used large div elements for the visual title. It looked like a heading, but semantically the page did not have an h1, so WAVE reported a missing first-level heading. I changed the hero title into an actual h1 while keeping the experimental visual layout of “DISCOVER”, “SOUND”, and “ROOMS”. WAVE also identified several missing labels on the Community post input and the Room Detail comment textarea. I fixed these by adding proper labels, including visually hidden `.sr-only` labels where I did not want the visual layout to change.

The most repeated accessibility issue was colour contrast. Many small metadata elements used light grey text such as #777 on white or off-white backgrounds, including post room labels, room details, playlist numbers, and discover card metadata. These were marked as low contrast, so I changed them to darker values to #333 and sometimes increased font weight. This kept the black-and-white visual style but made the interface easier to read. The AIM scores after these fixes were generally strong across the main pages, with all pages scoring above 9.0.

![Wave Evaluation of Homepage](assets/Wave-Evaluation-of-Homepage.png)
*Figure 1. Wave Evaluation of Homepage.*

![AIM accessibility scores](assets/Accessibility-Audit-Results.png)
*Figure 2. AIM accessibility scores across the main pages of Shen_ren.indie.music. All pages scored above 9.0.*

## Critical Reflection and Improvement Planning

One major reflection is that visual design alone won't work. At the beginning, I often solved problems page by page: making the homepage look stronger, improving the Browse cards, or adjusting the Profile and Community layouts. However, as more features were added, I realised that the real problem was the connection between pages. A room card was not only a visual object; it needed a database ID, image path, tag data, a route to its detail page, and consistent behaviour across the homepage, Browse page, and location recommendation section. Instead of designing each page as an isolated screen, I learned to think in terms of reusable data, shared components, and user flows. If I continued the project, I would plan these relationships earlier by mapping the main user journeys and ERD in a detailed way.

Another lesson was the importance of code organisation. As the project grew, the CSS became difficult to maintain because styles for the header, homepage, About, Browse, Community, Profile, Discover, and Room Detail pages were all in one large file. I reorganised the stylesheet into clearer sections for shared components and page-specific styles. This improved maintainability since I could find and edit styles quickly. It also made the project feel more professional, since layout rules, reusable classes, and page-specific rules had a clearer separation.

Accessibility should also have been considered earlier. Many WAVE issues appeared late in development because I focused first on visual style and then checked accessibility afterwards. If I worked on this project again, I would define accessible design rules earlier, such as minimum contrast colours for metadata, consistent label patterns for forms, and semantic heading structure for each page. This would reduce the need for late-stage fixes and make the interface stronger from the start.

If I continued the project, my improvement plan would focus on making existing features more complete than just adding more. The first priority would be to make the community system fully dynamic, so users can create posts, reply to specific rooms, and manage their own comments. The second priority would be to make the player functional rather than only visual. It will be functional and includes fast-forward, rewind, and room-switching features. The third priority would be performance and accessibility testing, including Lighthouse audits, lazy loading for images, keyboard navigation, and screen reader testing. These improvements are realistic because they build on the current structure instead of replacing it.

## Retrospective Assessment of Functional Requirements

I have to say my original functional requirements were mostly finished. The final prototype met the core requirements, but not always at the same level of completeness. The requirement for users to discover sound rooms was achieved through the homepage carousel, recommendation rows, and Discover page. The requirement for users to browse and filter rooms was achieved through the Browse page with genre, mood, and location filters. The requirement for users to view detailed room information was achieved through the Room Detail page. The profile requirement was also partly achieved because the logged-in user name appears in the header and profile page.

The community interaction was only partially finished due to time constraints and the workload. Users can submit a comment on a room detail page, which is stored into the database and can be shown accordingly on the page, but the page itself is still static. The audio player is also a visual prototype rather than a working music player. These limitations show that some of my initial requirements were too broad for the time available. In planning, “community interaction” sounded like one requirement, but in implementation it involved database relationships, routing, user identity, form handling, validation, and feedback. This made me realise that future requirements should be prioritised more carefully.

**But limitations are not always negative.**

They can reveal what should have been prioritised earlier. Because the project had a limited timeframe, we could not fully develop every feature to the same depth. This made me realise that a prototype needs clear levels of priority: some features should be fully functional, while others can remain as visual or conceptual demonstrations. At the same time, we really should have started development earlier, rather than waiting until the last few weeks to work frantically.

The project also taught me a lot about teamwork. Because we worked on different pages and components, consistency became a major challenge. Some pages used different CSS structures, different naming styles, or slightly different layouts, which later made integration more difficult. Through this, I learned that group work in web development is not only about dividing tasks, but also about agreeing on shared rules before everyone starts building. A shared design system, consistent class naming, reusable components, and clearer communication about routes and database fields would have reduced many problems after. Even though the final prototype is not production-ready, the process helped me understand how technical constraints, design decisions, and teamwork all affect the quality of a web application.