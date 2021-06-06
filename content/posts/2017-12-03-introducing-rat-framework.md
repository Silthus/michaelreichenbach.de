---
title: Introducing the RAT Framework
author: Michael
type: post
date: 2017-12-03T15:08:53+00:00
url: /introducing-rat-framework/
featured_image: /wp-content/uploads/2017/12/black-and-white-man-person-hands.jpg
categories:
  - Gamification
  - Programming
tags:
  - gamification
  - minecraft
  - programming
  - rat-framework

---
I first started designing the RAT Framework when programming plugins for [Minecraft][1]. At that time I needed a simple way to create achievements, conversations, quests and boss fights without hard coding everything into the plugins. I needed a way to outsource the logic into configuration files while maintaining the flexibility of a coded plugin. Thats when I came up with the RAT Framework. A framework to make everything meantioned above configurable, while splitting the needed programming logic into reuseable snippets of small code.

# What is the RAT Framework?

The **RAT** (**R**equirements **A**ctions **T**rigger) **Framework** provides an intuitive way to define multiple actions, triggers and requirements and reuse them in configration files loaded up and parsed as needed. It defines a clear pattern to use for communication between components. And it also provides two configuration languages that can be used to create readable configuration files in YAML or JSON. The framework will also provide a way to share actions and triggers accross platforms and technologies. Making it possible to achieve complex cross platform tasks (like achievements) in a single configuration file.

## Trigger

Triggers are the fundamental building block and the source for everything inside the RAT framework. A trigger can be as simple as someone clicking a button or as complex as a person walking into the radius of defined coordinates. They already exist in many programming languages known as events. The RAT Framework will reuse those events and provide a way to use them in configuration files.

## Requirements

Actions and Triggers both can have requirements that need to be satisfied before an action or trigger is executed. An example for this would be a user clicking a specific button or entering a defined country.

## Actions

Actions are the last building block and as the name suggests the active part of the RAT Framework. When you give out a reward you basically execute a list of specific actions. Also inside games this could be used to orchastrate boss fights and special attacks of the boss.

## The Configuration

The central part of the RAT Framework is the common configuration syntax. It makes it possible to define even the most complex tasks in a couple of lines. Here YAML is used as the base and therefor JSON is also a valid config file format.

See each of the links above to learn more about the individual parts. Also over time I will Open Source parts of the framework so you can use the awesomenes in your own projects. I will also heavly utilize this framework in my [HöhenSucht][2] project to gamify the experience.

 [1]: http://www.raid-craft.de
 [2]: https://michaelreichenbach.de/5-kriterien-eines-modernen-tourenbuchs/