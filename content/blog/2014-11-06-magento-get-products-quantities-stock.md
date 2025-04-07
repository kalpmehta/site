---
id: 959
title: 'Magento: Get all products with quantities and Out Of Stock'
date: '2014-11-06T20:27:28+00:00'
author: kalpesh
layout: post
tags:
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