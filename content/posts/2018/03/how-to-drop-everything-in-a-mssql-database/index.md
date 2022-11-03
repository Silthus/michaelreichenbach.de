---
title: How to drop everything in a MS SQL Database
date: 2018-03-13
url: /posts/how-to-drop-everything-in-a-mssql-database/
categories:
  - Programming
  - System Administration
tags:
  - script
  - sql
---
When working with SQL data and lots of foreign keys, you may have the need to drop everything. Well I have just the right SQL statement for you. The following statement will drop everything the given database, including the following:

- non-system stored procedures
- views
- functions
- foreign key constraints
- primary key constraints
- tables

You can execute parts of the script on its own if you only want to drop a certain part.

## Drop everything in a MSSQL database

The SQL script must be execute on the database level. Optionally you can add an USE `YOUR_DATABASE_NAME` statement on the top.

{{< gist Silthus 3dae25b8546f2fb2c8f45becf635d78b >}}

## Update 07.01.2019

I added the option to iterate over all schemas in the selected database and drop everything in every schema including the schema.

{{< gist Silthus 0159df3b4ee826cfb289b0572414179b >}}

You can also find more solutions, including this one, [on stackoverflow][1].

 [1]: https://stackoverflow.com/questions/27606518/how-to-drop-all-tables-from-a-database-with-one-sql-query/49259751#49259751