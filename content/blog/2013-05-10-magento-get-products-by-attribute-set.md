---
id: 591
title: 'Magento get products by attribute set id or name'
date: '2013-05-10T19:18:29+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'attribute set'
    - magento
    - product
---

In Magento get all the products by specific attribute set ID or Name with below code snippet. If you want to get products by attribute set Name, then first get the attribute set ID from name as shown in the first 4 lines of code. If you already have attribute set ID, ignore first 4 lines of code as it is only used if you have attribute set Name and not it’s ID.

The resultant array will give you all the products with all the attributes and values. You can narrow the attributes that you only need by specifying them when you call *$products->addAttributeToSelect(*)* or when you get all data from product *$prod->getData()*.

{{< highlight php "style=emacs" >}}//If planning to get all products by attribute set NAME  
$attrSetName = ‘your_attribute_set_name_here’;  
$attributeSetId = Mage::getModel(‘eav/entity_attribute_set’)  
 ->load($attrSetName, ‘attribute_set_name’)  
 ->getAttributeSetId();

//If planning to get all products by attribute set ID  
$attributeSetId = ‘your_attribute_set_id_here’;

$products = Mage::getModel(‘catalog/product’)->getCollection();  
$products->addAttributeToFilter(‘attribute_set_id’,$attributeSetId);

$products->addAttributeToSelect(‘*’);

$products->load();  
foreach($products as $prod) {  
 $productsArray[] = $prod->getData(); //get all data or specify any attribute  
}

Mage::log($productsArray());{{< /highlight >}}