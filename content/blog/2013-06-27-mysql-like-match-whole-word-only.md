---
id: 742
title: 'MYSQL LIKE match whole word only'
date: '2013-06-27T11:40:15+00:00'
author: kalpesh
layout: post
tags:
    - MySQL
tags:
    - mysql
---

Mysql LIKE clause match exact whole word only while searching. Search the words with space in mysql database.

If you want to search for exact word using LIKE clause, you can’t do it just using percentage (%) sign around the keyword as it will search for partial words too. For example, the below query will match all the words which contain “some”:

{{< highlight mariadb "style=emacs" >}}SELECT * FROM tablename WHERE columnname LIKE ‘%some%’;{{< /highlight >}}

It will find all the instances where it finds *some*, as a whole or a part. some, someone, something, handsome, isometric are all MATCHED using above query. Ofcourse there will be many results which are UNRELATED.

But what if you only want *some*, as an exact word WITH space and WITHOUT any extra heading and trailing characters?

This query will do exactly that:

{{< highlight mariadb "style=emacs" >}}SELECT * FROM tablename WHERE columnname = ‘some’ OR columnname LIKE ‘% some’ OR columnname LIKE ‘some %’ OR columnname LIKE ‘% some %’;{{< /highlight >}}

In above query we are making sure that all the *some* instances are retrieved, whether they are present in the START or in the END or in the MIDDLE of the columnname field.