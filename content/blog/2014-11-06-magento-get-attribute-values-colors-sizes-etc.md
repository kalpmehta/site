---
id: 963
title: 'Magento: Get all attribute values (colors, sizes, etc..)'
date: '2014-11-06T20:44:48+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=963'
permalink: /index.php/2014/11/06/magento-get-attribute-values-colors-sizes-etc/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-options/"     class="crp_title">Magento get attribute options</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li><li><a href="http://ka.lpe.sh/2013/08/13/magento-convert-attribute-type-from-text-to-dropdown/"     class="crp_title">Magento convert attribute type from TEXT to DROPDOWN</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-label/"     class="crp_title">Magento get attribute label</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li></ul></div>'
categories:
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