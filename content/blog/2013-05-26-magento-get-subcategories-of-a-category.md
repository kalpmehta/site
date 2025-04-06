---
id: 655
title: 'Magento get subcategories of a category by category ID'
date: '2013-05-26T17:13:56+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=655'
permalink: /index.php/2013/05/26/magento-get-subcategories-of-a-category/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li></ul></div>'
categories:
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