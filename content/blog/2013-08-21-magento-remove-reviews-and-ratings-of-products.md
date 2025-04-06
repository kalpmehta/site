---
id: 837
title: 'Magento remove reviews and ratings of products'
date: '2013-08-21T21:38:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=837'
permalink: /index.php/2013/08/21/magento-remove-reviews-and-ratings-of-products/
snapEdIT:
    - '1'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/08/09/magento-how-to-delete-remove-all-products-from-all-categories/"     class="crp_title">Magento: How to delete/remove all products from all categories</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/"     class="crp_title">WordPress: Show total/aggregate ratings and reviews to your posts/pages</a></li><li><a href="http://ka.lpe.sh/2012/07/24/mysql-delete-duplicate-records/"     class="crp_title">Mysql delete duplicate records leaving one</a></li><li><a href="http://ka.lpe.sh/2013/07/16/magento-get-products-without-category/"     class="crp_title">Magento get products without category</a></li></ul></div>'
snapFB:
    - 's:302:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200581557885680";s:5:"pDate";s:19:"2013-08-21 21:38:31";}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"370298895802585088";s:5:"pDate";s:19:"2013-08-21 21:38:31";}}";'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5776064587958845440&amp;type=U&amp;a=u9nR";s:5:"pDate";s:19:"2013-08-21 21:38:31";}}";'
categories:
    - Magento
---

Magento don’t provide admin screen where store owner can delete all the reviews and ratings of the products. The easiest way to delete them is using raw SQL queries, which you can run in Mysql console or in PhpMyAdmin. Remove/delete all the reviews and ratings of products in Magento using simple SQL queries given below.

{{< highlight mariadb "style=emacs" >}}truncate table `rating_option_vote`;  
truncate table `rating_option_vote_aggregated`;  
truncate table `review`;  
truncate table `review_detail`;  
truncate table `review_entity_summary`;  
truncate table `review_store`;{{< /highlight >}}