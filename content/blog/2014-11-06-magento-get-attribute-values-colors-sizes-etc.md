---
id: 963
title: 'Magento: Get all attribute values (colors, sizes, etc..)'
date: '2014-11-06T20:44:48+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - attribute
    - magento
    - values
---

Magento get all the attribute values you have in the store. Get all the colors and sizes values in Magento. Change the attribute name to whatever you want values for, in the below script.

{{< highlight php "style=emacs" >}}require_once(‘app/Mage.php’);  
umask(0);  
Mage::app(‘admin’);  
//set_time_limit(0);  
$attribute = Mage::getModel(‘eav/config’)->getAttribute(‘catalog_product’, ‘color’);  
$colors = array();  
foreach ($attribute->getSource()->getAllOptions(true) as $option) {  
 $colors[] = $option[‘label’];  
}  
sort($colors);  
foreach($colors as $lbl) {  
 echo “<span style="background-color:lightgrey">“.$lbl . “</span>“;  
 echo “  
“;  
}{{< /highlight >}}

Replace *color* with any attribute you want to get values for. Above script also sorts the result set in alphabetic order to make it easy to view all values. If you don’t want to sort the values, just comment out the line which sorts it.