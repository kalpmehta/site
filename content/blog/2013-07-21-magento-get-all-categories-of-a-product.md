---
id: 800
title: 'Magento get all categories of a product'
date: '2013-07-21T15:44:40+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=800'
permalink: /index.php/2013/07/21/magento-get-all-categories-of-a-product/
snapEdIT:
    - '1'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5764741700824072192&amp;type=U&amp;a=TyT1";s:5:"pDate";s:19:"2013-07-21 15:45:25";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"358976007862091778";s:5:"pDate";s:19:"2013-07-21 15:45:24";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-get-subcategories-of-a-category/"     class="crp_title">Magento get subcategories of a category by category ID</a></li><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li></ul></div>'
snapFB:
    - 's:302:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200416497799281";s:5:"pDate";s:19:"2013-07-21 15:45:29";}}";'
categories:
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