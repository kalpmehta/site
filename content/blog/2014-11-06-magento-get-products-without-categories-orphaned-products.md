---
id: 953
title: 'Magento: Get all products without categories (orphaned products)'
date: '2014-11-06T20:17:43+00:00'
author: kalpesh
layout: post
tags:
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