---
id: 355
title: 'Magento Get most popular products in a category'
date: '2012-10-18T12:34:02+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=355'
permalink: /index.php/2012/10/18/magento-get-most-popular-products-in-a-category/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - category
    - magento
    - popular
    - products
    - sold
---

Magento get most popular products in any specified category using below code, you can show them in the sidebar of product detail page to let your visitors know the popularity of the products for that category.

{{< highlight php "style=emacs" >}}$category = Mage::getModel(‘catalog/category’)->load($categoryId);  
$products = Mage::getResourceModel(‘reports/product_collection’)  
 ->addOrderedQty() //total number of quantities ordered  
 ->addAttributeToSelect(‘*’) //get all attributes  
 ->setOrder(‘ordered_qty’, ‘desc’) //most ordered quantity products first  
 ->addCategoryFilter($category);{{< /highlight >}}