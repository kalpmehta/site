---
id: 830
title: 'Magento delete empty categories and sub-categories'
date: '2013-08-17T14:36:45+00:00'
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