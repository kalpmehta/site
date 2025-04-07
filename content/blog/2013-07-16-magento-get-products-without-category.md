---
id: 765
title: 'Magento get products without category'
date: '2013-07-16T13:12:09+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - MySQL
tags:
    - magento
    - 'orphaned products'
---

Get a list of all orphaned products which are not associated with any category in Magento. Sometimes you may have missed to select categories for products by mistake when filling new product details, and now want to list them and assign categories to those products. You can’t get it from the Magento admin screen so you will need to run below MySQL query to get all the products without categories.

{{< highlight mariadb "style=emacs" >}}SELECT e.entity_id, e.sku, e.name FROM catalog_product_entity AS e LEFT JOIN catalog_category_product AS cp ON cp.product_id = e.entity_id WHERE cp.category_id IS NULL{{< /highlight >}}

Above sql query will simply bring the product ID, SKU, Name of products where category is NULL. You can add more columns in select (like e.*) to list full details of products.