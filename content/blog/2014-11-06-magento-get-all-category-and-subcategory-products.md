---
id: 961
title: 'Magento: Get all category and subcategory products'
date: '2014-11-06T20:37:45+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=961'
permalink: /index.php/2014/11/06/magento-get-all-category-and-subcategory-products/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-all-categories-of-a-product/"     class="crp_title">Magento get all categories of a product</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-get-subcategories-of-a-category/"     class="crp_title">Magento get subcategories of a category by category ID</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-display-categories-subcategories/"     class="crp_title">Magento display categories and sub-categories</a></li><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - category
    - magento
    - products
    - subcategory
---

Magento get all category and subcategory products which are assigned to categories at different levels. Below script will show you all the categories, and all the associated product names under each of those categories.

{{< highlight php "style=emacs" >}}<?php require_once('app/Mage.php');
umask(0);
Mage::app('admin');
set_time_limit(0);

$category = Mage::getModel('catalog/category');
$tree = $category->
getTreeModel();  
$tree->load();

$ids = $tree->getCollection()->getAllIds();

if ($ids)  
{  
 foreach ($ids as $id)  
 {  
 $cat = Mage::getModel(‘catalog/category’);  
 $cat->load($id);  
 if($cat->getLevel()==3 &amp;&amp; $cat->getIsActive()==1)  
 {  
 $category1 = Mage::getModel(‘catalog/category’)->load($cat->getId());  
 $products = Mage::getResourceModel(‘catalog/product_collection’)  
 ->addAttributeToSelect(‘name’)  
 ->addCategoryFilter($category1);  
 echo “**“.$cat->getName().”**  
“;  
 foreach ($products as $product) { //print_r($product->getData());exit;  
 echo ” ” . $product->getName() . ” – “. $product->getSku() . “  
“;  
 }  
 }  
 }  
}  
?>{{< /highlight >}}

Note the line which checks category getLevel()==3, you can change this line to get different subcategory levels by adjusting it.  
For root category, getLevel() should be 1.  
For all the main/primary categories, getLevel() should be 2.  
For all the subcategories, getLevel() should be 3.  
For all the subsubcategories, getLevel() should be 4.  
and so on…

Above script will get you all the category and subcategories products, products assigned to each and every categories of your store.