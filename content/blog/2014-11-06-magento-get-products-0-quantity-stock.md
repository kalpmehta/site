---
id: 957
title: 'Magento: Get all products with 0 quantity and In Stock'
date: '2014-11-06T20:23:39+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'in stock'
    - magento
    - products
    - 'zero quantity'
---

Magento get all products which have zero quantity and are still In Stock in inventory. Below script will show you all such simple products.

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
 ‘{{table}}.is_in_stock=1’,  
 ‘left’)  
 ->addAttributeToFilter(‘qty’, array(“eq” => 0));

echo “

## Simple Products with 0 quantity and In Stock

“;  
foreach($productCollection as $product) { //print_r($product->getData());exit;  
 if($product->getTypeId() == ‘simple’)  
 echo $product->getName() . ” | ” . $product->getSku() . “  
“;  
}  
echo ‘Done’;  
?>{{< /highlight >}}