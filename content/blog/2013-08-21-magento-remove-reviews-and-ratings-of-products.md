---
id: 837
title: 'Magento remove reviews and ratings of products'
date: '2013-08-21T21:38:16+00:00'
author: kalpesh
layout: post
tags:
    - Magento
---

Magento don’t provide admin screen where store owner can delete all the reviews and ratings of the products. The easiest way to delete them is using raw SQL queries, which you can run in Mysql console or in PhpMyAdmin. Remove/delete all the reviews and ratings of products in Magento using simple SQL queries given below.

{{< highlight mariadb "style=emacs" >}}truncate table `rating_option_vote`;  
truncate table `rating_option_vote_aggregated`;  
truncate table `review`;  
truncate table `review_detail`;  
truncate table `review_entity_summary`;  
truncate table `review_store`;{{< /highlight >}}