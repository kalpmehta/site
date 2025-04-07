---
id: 316
title: 'Mysql: Find column name in any table(s) having it in whole database'
date: '2012-08-03T15:31:53+00:00'
author: kalpesh
layout: post
tags:
    - MySQL
tags:
    - mysql
    - 'search column in database'
---

There may be instances where we want to find in how many tables of some particular database some column (field) occurs. Or you know that some column field existed but don’t remember in which table of a database, what will you do? And if there are hundreds of tables, it would be nightmare to go through each table schema and searching.

Below Mysql query will get you all the tables where the specified column occurs in some database.  
{{< highlight mariadb "style=emacs" >}}SELECT table_name, column_name from information_schema.columns WHERE column_name LIKE ‘%column_name_to_search%’;{{< /highlight >}}  
Remember, don’t use % before column_name_to_search if you know the starting characters of that column. It slows down, as Mysql will not use any indexes for fields searched with leading wildcard (%).