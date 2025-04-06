---
id: 664
title: 'Magento filter products by status'
date: '2013-05-26T18:35:49+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=664'
permalink: /index.php/2013/05/26/magento-filter-products-by-status/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - magento
    - product
    - status
---

Get all the products with status equal to enabled/disabled.

If you are using Flat Catalog in Magento, you will not get disabled products by this filter as in flat table all the products are only enabled one. You can check if your Magento website uses flat catalog or not by going here:  
*Admin > System > Configuration > Catalog section > Catalog > Frontend*

Check *Use Flat Catalog Category* and *Use Flat Catalog Product*, if they are *Yes* it means you are using flat catalog, if they are *No* it means you are NOT using flat catalog.

So, if you don’t have flat catalog enabled and you want to filter all the products with status equal to disabled, you can use below code:

{{< highlight php "style=emacs" >}}$products = Mage::getModel(‘catalog/category’)->load($category_id)  
->getProductCollection()  
->addAttributeToSelect(‘*’) //whatever attributes you want to get here  
->addAttributeToFilter(  
 ‘status’,  
 array(‘eq’ => Mage_Catalog_Model_Product_Status::STATUS_DISABLED)  
 //replace DISABLED to ENABLED for products with status enabled  
);{{< /highlight >}}