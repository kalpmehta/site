---
id: 959
title: 'Magento: Get all products with quantities and Out Of Stock'
date: '2014-11-06T20:27:28+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=959'
permalink: /index.php/2014/11/06/magento-get-products-quantities-stock/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/11/06/magento-get-products-0-quantity-stock/"     class="crp_title">Magento: Get all products with 0 quantity and In Stock</a></li><li><a href="http://ka.lpe.sh/2014/11/06/magento-get-products-without-categories-orphaned-products/"     class="crp_title">Magento: Get all products without categories (orphaned products)</a></li><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
    - 'out of stock'
    - products
---

Magento get all the simple products which have greater than 0 quantity and are still Out of Stock in inventory.

{{< highlight php "style=emacs" >}}<?php require_once('app/Mage.php');
umask(0);
Mage::app('admin');
set_time_limit(0);

$productCollection = Mage::getModel('catalog/product')
     ->
getCollection()  
 ->addAttributeToSelect(‘*’)  
 ->joinField(‘qty’,  
 ‘cataloginventory/stock_item’,  
 ‘qty’,  
 ‘product_id=entity_id’,  
 ‘{{table}}.is_in_stock=0’,  
 ‘left’)  
 ->addAttributeToFilter(‘qty’, array(“gt” => 0));

echo “

## Simple Products with >0 quantity and Out of Stock

“;  
foreach($productCollection as $product) { //print_r($product->getData());exit;  
 if($product->getTypeId() == ‘simple’)  
 echo $product->getName() . ” | ” . $product->getSku() . “  
“;  
}  
echo ‘Done’;  
?>{{< /highlight >}}