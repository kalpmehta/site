---
id: 953
title: 'Magento: Get all products without categories (orphaned products)'
date: '2014-11-06T20:17:43+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=953'
permalink: /index.php/2014/11/06/magento-get-products-without-categories-orphaned-products/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/16/magento-get-products-without-category/"     class="crp_title">Magento get products without category</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
    - 'no categories'
    - orphaned
    - products
---

Magento get all the configurable/simple products which are not associated with any categories, which are orphaned products. To get all the products (regardless of their type), simply ignore the condition where it checks for type_id in the below query and comment the condition line in foreach loop.

Below script will get all such products, you can create new PHP file at the root of Magento installation and paste the code:

{{< highlight php "style=emacs" >}}<?php require_once('app/Mage.php');
umask(0);
Mage::app('admin');
set_time_limit(0);

$i=0;
$sql = "select
    type_id,sku
 from catalog_product_entity a
 left join catalog_category_product cp on cp.`product_id` = a.entity_id
 left join catalog_product_relation cpr on cpr.child_id = a.entity_id
 where
       cp.product_id is null
   and cpr.parent_id is null
   and a.type_id = 'configurable'";
$connection = Mage::getSingleton('core/resource')->
getConnection(‘core_read’);  
//echo count($connection->fetchAll($sql));exit;

foreach ($connection->fetchAll($sql) as $arr_row) {  
 $pid = $arr_row[‘sku’];  
 $product = Mage::getModel(‘catalog/product’)->loadByAttribute(‘sku’,$pid);  
 if($product->getTypeId()!=’configurable’) continue;  
 $i++;  
 echo $i .”) “. $product->getName() . ” – ” . $product->getSku() . “  
“;  
}  
?>{{< /highlight >}}