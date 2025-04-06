---
id: 296
title: 'Mysql delete duplicate records leaving one'
date: '2012-07-24T17:22:49+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=296'
permalink: /index.php/2012/07/24/mysql-delete-duplicate-records/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/08/09/magento-how-to-delete-remove-all-products-from-all-categories/"     class="crp_title">Magento: How to delete/remove all products from all categories</a></li><li><a href="http://ka.lpe.sh/2012/07/12/magento-add-radio-checkbox-button-to-admin-grid/"     class="crp_title">Magento add radio / checkbox button to admin grid</a></li><li><a href="http://ka.lpe.sh/2012/10/10/ubuntu-delete-temporary-cache-files/"     class="crp_title">Ubuntu: Delete temporary/cache files</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li></ul></div>'
categories:
    - MySQL
tags:
    - delete
    - 'duplicate records'
    - mysql
    - remove
---

Mysql delete duplicate records leaving one row. Consider that there are many duplicate records in the table and you want to remove it. Now, we can select it by applying GROUP BY but the question is how to delete all the duplicate records (of field some_id below) EXCEPT one that should be there. So, lets say I have following table with duplicate data as shown:  
**Tablename: test**  
{{< highlight sql "style=emacs" >}}   
unique_id | some_id  
——————–  
1 | 1  
2 | 1  
3 | 2  
4 | 2  
5 | 1  
{{< /highlight >}}  
  
Solution:  
{{< highlight sql "style=emacs" >}} DELETE t1 FROM test t1, test t2 WHERE t1.unique_id > t2.unique_id AND t1.some_id = t2.some_id;{{< /highlight >}}

Final Result:  
{{< highlight sql "style=emacs" >}}   
unique_id | some_id  
——————–  
1 | 1  
3 | 2  
{{< /highlight >}}