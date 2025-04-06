---
id: 742
title: 'MYSQL LIKE match whole word only'
date: '2013-06-27T11:40:15+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=742'
permalink: /index.php/2013/06/27/mysql-like-match-whole-word-only/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/08/03/mysql-find-column-name-in-any-tables-having-it-in-whole-database/"     class="crp_title">Mysql: Find column name in any table(s) having it in whole database</a></li><li><a href="http://ka.lpe.sh/2012/04/18/magento-get-sentence-case-from-camel-case-string/"     class="crp_title">Magento: Get sentence case from camel case string</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-reset-download-limit-for-downloadable-product-item-order/"     class="crp_title">Magento: Reset download limit for downloadable product item/order</a></li><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-check-availability-of-domain-names-in-differnet-tlds/"     class="crp_title">Linux: Bash script to check availability of domain names in differnet TLDs</a></li><li><a href="http://ka.lpe.sh/2013/05/23/magento-clone-collection-how-to-clone-collection-in-magento/"     class="crp_title">Magento clone collection &#8211; How to clone collection in Magento</a></li></ul></div>'
categories:
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