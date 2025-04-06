---
id: 830
title: 'Magento delete empty categories and sub-categories'
date: '2013-08-17T14:36:45+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=830'
permalink: /index.php/2013/08/17/magento-delete-empty-categories-and-sub-categories/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snap_isAutoPosted:
    - '1'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5774508982836150272&amp;type=U&amp;a=yDcU";s:5:"pDate";s:19:"2013-08-17 14:37:06";}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"368743295255465984";s:5:"pDate";s:19:"2013-08-17 14:37:07";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-all-categories-of-a-product/"     class="crp_title">Magento get all categories of a product</a></li><li><a href="http://ka.lpe.sh/2013/07/16/magento-get-products-without-category/"     class="crp_title">Magento get products without category</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - category
    - magento
    - product
---

Remove all empty categories and sub-categories in Magento. When there are empty categories, the website shows empty page in those categories in frontend. Create a file in the magento root, I will name it rmvEmptyCats.php, with following code:

{{< highlight php "style=emacs" >}}require “app/Mage.php”;  
umask(0);  
Mage::app();

$categoryCollection = Mage::getModel(‘catalog/category’)->getCollection()  
 ->addFieldToFilter(‘level’, array(‘gteq’ => 2)); //greater than root category id

foreach($categoryCollection as $category) {  
 if ($category->getProductCount() === 0) {  
 $category->delete();  
 }  
}

echo ‘Empty Categories Deleted!’;{{< /highlight >}}

Now you can easily run it by navigating to http://loca.lho.st/rmvEmptyCats.php and wait for the message Empty Categories Deleted!

Note that this is going to DELETE those categories with zero product count.