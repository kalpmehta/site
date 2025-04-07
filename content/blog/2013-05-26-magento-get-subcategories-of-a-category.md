---
id: 655
title: 'Magento get subcategories of a category by category ID'
date: '2013-05-26T17:13:56+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
---

Get all the subcategories of any category in Magento.

If you have a category ID (current category OR any category) then you can easily get all the subcategories of that particular category.

Below code will load all the subcategories of the current category. You can even get all the subcategories of any specific category by assigning category ID to $catID.

{{< highlight php "style=emacs" >}}$catID = $current_category->getId(); //or any specific category id, e.g. 5  
$children = Mage::getModel(‘catalog/category’)->getCategories($catID);  
foreach ($children as $category) {  
 echo $category->getId();  
 echo $category->getName();  
 echo $category->getRequestPath();  
 print_r($category->getData());  
}{{< /highlight >}}