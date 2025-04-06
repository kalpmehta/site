---
id: 316
title: 'Mysql: Find column name in any table(s) having it in whole database'
date: '2012-08-03T15:31:53+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=316'
permalink: /index.php/2012/08/03/mysql-find-column-name-in-any-tables-having-it-in-whole-database/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2013/04/18/pdo_mysql-extension-is-not-installed/"     class="crp_title">pdo_mysql extension is not installed</a></li></ul></div>'
categories:
    - MySQL
tags:
    - mysql
    - 'search column in database'
---

There may be instances where we want to find in how many tables of some particular database some column (field) occurs. Or you know that some column field existed but don’t remember in which table of a database, what will you do? And if there are hundreds of tables, it would be nightmare to go through each table schema and searching.

Below Mysql query will get you all the tables where the specified column occurs in some database.  
{{< highlight mariadb "style=emacs" >}}SELECT table_name, column_name from information_schema.columns WHERE column_name LIKE ‘%column_name_to_search%’;{{< /highlight >}}  
Remember, don’t use % before column_name_to_search if you know the starting characters of that column. It slows down, as Mysql will not use any indexes for fields searched with leading wildcard (%).