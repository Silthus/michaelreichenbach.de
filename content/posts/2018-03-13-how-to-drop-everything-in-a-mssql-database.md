---
title: How to drop everything in a MS SQL Database
author: Michael
type: post
date: 2018-03-13T15:26:21+00:00
url: /how-to-drop-everything-in-a-mssql-database/
featured_image: /wp-content/uploads/2018/03/nuclear-weapons-test-nuclear-weapon-weapons-test-explosion-73909.jpeg
categories:
  - Programming
  - System Administration
tags:
  - script
  - sql

---
When working with SQL data and lots of foreign keys, you may have the need to drop everything. Well I have just the right SQL statement for you. The following statement will drop everything the given database, including the following:

  * non-system stored procedures
  * views
  * functions
  * foreign key constraints
  * primary key constraints
  * tables

You can execute parts of the script on its own if you only want to drop a certain part.

# Drop everything in a MSSQL database

The SQL script must be execute on the database level. Optionally you can add an USE &#8216;YOUR\_DATABASE\_NAME&#8217; statement on the top.

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Silthus/3dae25b8546f2fb2c8f45becf635d78b">Gist</a>.
  </noscript>
</div>

### Update 07.01.2019

I added the option to iterate over all schemas in the selected database and drop everything in every schema including the schema.

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Silthus/0159df3b4ee826cfb289b0572414179b">Gist</a>.
  </noscript>
</div>

&nbsp;