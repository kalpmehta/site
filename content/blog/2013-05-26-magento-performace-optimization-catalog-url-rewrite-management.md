---
id: 647
title: 'Magento performace optimization, Catalog URL Rewrite Management'
date: '2013-05-26T15:56:17+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=647'
permalink: /index.php/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/26/magento-remove-index-php-from-url/"     class="crp_title">Magento remove index.php from URL</a></li><li><a href="http://ka.lpe.sh/2012/08/09/magento-how-to-delete-remove-all-products-from-all-categories/"     class="crp_title">Magento: How to delete/remove all products from all categories</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li></ul></div>'
categories:
    - Magento
    - Performance
tags:
    - magento
---

If your Magento site is slow, then one of the reason can be because of Catalog URL Rewrites. You can check in the Magento Admin > Catalog > URL Rewrite Management. If you see the catalog rewrites are very large than expected as per total Categories and Products you have, this will create your site to be slow. This generally gets too large if you edit the categories/products and change it’s URL. Generally we keep on changing the product URL to optimize for search engines or to correct some typo in the link. Magento saves all the previous category and product URLs even if it is changed many times, resulting in more number of URL rewrites in database. I have seen in one of the project, where total SKUs were near to 4,00,000 while the URL Rewrites were near to 46,00,000 with just one website and store!

![Magento Catalog URL Rewrite Management](http://ka.lpe.sh/wp-content/uploads/2013/05/Catalog_URL_Rewrite_Management.png)  
  
**Solution:**  
– First step is ofcourse, to take the backup of table core_url_rewrite  
If something goes wrong then we can restore our old core_url_rewrite table to bring it back.

– Now truncate the table core_url_rewrite  
*truncate table core_url_rewrite* in your Mysql console or from phpMyAdmin to empty this table.

– Re-index “Catalog URL Rewrite” from Index Management  
This will create all the URL rewrites (current URLs only) for your categories and products and insert it into core_url_rewrite table.