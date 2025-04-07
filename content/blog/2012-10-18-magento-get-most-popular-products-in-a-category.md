---
id: 355
title: 'Magento Get most popular products in a category'
date: '2012-10-18T12:34:02+00:00'
author: kalpesh
layout: post
tags:
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