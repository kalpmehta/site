---
id: 765
title: 'Magento get products without category'
date: '2013-07-16T13:12:09+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=765'
permalink: /index.php/2013/07/16/magento-get-products-without-category/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-filter-products-by-status/"     class="crp_title">Magento filter products by status</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li></ul></div>'
categories:
    - Magento
    - MySQL
tags:
    - magento
    - 'orphaned products'
---

Get a list of all orphaned products which are not associated with any category in Magento. Sometimes you may have missed to select categories for products by mistake when filling new product details, and now want to list them and assign categories to those products. You can’t get it from the Magento admin screen so you will need to run below MySQL query to get all the products without categories.

{{< highlight mariadb "style=emacs" >}}SELECT e.entity_id, e.sku, e.name FROM catalog_product_entity AS e LEFT JOIN catalog_category_product AS cp ON cp.product_id = e.entity_id WHERE cp.category_id IS NULL{{< /highlight >}}

Above sql query will simply bring the product ID, SKU, Name of products where category is NULL. You can add more columns in select (like e.*) to list full details of products.