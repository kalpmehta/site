---
id: 800
title: 'Magento get all categories of a product'
date: '2013-07-21T15:44:40+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - category
    - magento
    - product
---

Get all the categories a product belongs to in Magento. Below code will get you all the categories with details the product is attached to. Product can be shown under more than one category, so you may get more than one category ID. Either get the category collection from product, or get all the category IDs and then load them using catalog category collection model.

{{< highlight php "style=emacs" >}}//$_product = Mage::getModel(‘catalog/product’)->load($productID);{{< /highlight >}}

First way,  
{{< highlight php "style=emacs" >}}$catCollection = $_product->getCategoryCollection();  
foreach($catCollection as $cat){  
 print_r($cat->getData());  
 //echo $cat->getName();  
 //echo $cat->getUrl();  
}{{< /highlight >}}

Another way,  
{{< highlight php "style=emacs" >}}$catIds = $_product->getCategoryIds();  
$catCollection = Mage::getResourceModel(‘catalog/category_collection’)  
 //->addAttributeToSelect(‘name’)  
 //->addAttributeToSelect(‘url’)  
 ->addAttributeToSelect(‘*’)  
 ->addAttributeToFilter(‘entity_id’, $catIds)  
 ->addIsActiveFilter();

foreach($catCollection as $cat){  
 print_r($cat->getData());  
 //echo $cat->getName();  
 //echo $cat->getUrl();  
}{{< /highlight >}}