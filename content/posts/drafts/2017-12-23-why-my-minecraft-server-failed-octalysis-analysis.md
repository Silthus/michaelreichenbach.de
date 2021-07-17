---
title: Why my Minecraft server failed – an Octalysis analysis
author: Michael
type: post
draft: true
date: 2017-12-23T17:40:57+00:00
url: /why-my-minecraft-server-failed-octalysis-analysis/
categories:
  - Personal
  - Projects
tags:
  - minecraft
  - octalysis
  - raid-craft

---
Back in 2010 I founded the Minecraft server [Raid-Craft][1] which three years later turned out to be quite successful with over 50 users online at the same time. However at one point I made a decision wich would lead the server to its downfall. Almost 4 years later I learned about the [Octalysis Framework][2] and if I had that knowledge at that time my decision definitly would have been a different one.

# The Vision

To understand the following analysis, we must first understand what the Minecraft server was about.  
Raid-Craft was originally only a server for friends that wanted to play together. However as I was learning to program Minecraft plugins I wanted to try out more and more. So it came that we started customizing the server with plugins that would manage real estate properties, currencies and events.

With time my skills improved and I more and more learned what awesome stuff could be done with plugins. I am also a huge fans of MMORPGs and played World of Warcraft for a very long time. So it came that I wanted to develop an awesome experience as close as possible to huge MMORPGs like WoW. However I made one huge mistake&#8230;

# The Mistake

In 2013 Raid-Craft was at its best. We had over 100 active users and at peak hours 50 or more users would be online at the same time. Everyone was having fun, there were custom minigames and events every weekend and the community was flourishing. In October 2013 Minecraft 1.7 was released and parts of our world was completly destroyed. Thats when I decided not to invest energy into repairing the world but making a hard cut and launch the new RPG system we developed. As a result our player base broke away and the server went to hell. It didnt matter that we implemented a custom skillsystem with 8 classes, quests, custom items, achievements, flying dragons and much more. We even programmed an importer for WoW items and copied ALL, yes ALL items from vanilla World of Warcraft into Minecraft.

> The problem: we copied only &#8220;the shell and not the essence&#8221;.

For all of those that played and loved Raid-Craft as it was back then: I am so sorry, I did not listen to the community and destroyed the server.

# The Analysis

When I think back it is now obvious to me what went wrong back then. Like Yu-kai Chou writes in his book [&#8220;<span id="ebooksProductTitle" class="a-size-extra-large">Actionable Gamification: Beyond Points, Badges, and Leaderboards&#8221;</span>][3] about copying only the shell and not the esence, it became clear to me that I made exactly that mistake &#8211; I copied only the shell from World of Warcraft but completly missed out on the essence.

We also took away a lot of freedom and the possiblity of creativity (CD3) by constraining the players into a handcrafted world where they could hardly build anything. Coupled with the loss of their old buildings (CD8) we had two very powerful anti core drives working against us. We should have tried to recover the old world and built upon the existing while listening to our users.

In the end it always comes down to the **why** and **not** the **what**. Thats what we did wrong.

 [1]: http://raid-craft.de
 [2]: http://yukaichou.com/gamification-examples/octalysis-complete-gamification-framework/
 [3]: https://www.amazon.com/Actionable-Gamification-Beyond-Points-Leaderboards-ebook/dp/B00WAOGY4U