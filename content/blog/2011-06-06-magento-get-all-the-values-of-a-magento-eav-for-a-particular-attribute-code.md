---
id: 38
title: 'Magento: Get all the values of a Magento EAV for a particular attribute code'
date: '2011-06-06T10:12:18+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - attribute
    - EAV
    - magento
    - product
    - value
---

If you have ever wondered how to get all the values of any EAV attribute for products in Magento, then this is the workaround for you:

{{< highlight php "style=emacs" >}}$attribute = Mage::getModel(‘eav/config’)->getAttribute(‘catalog_product’, ‘color’); //here, “color” is the attribute_code  
$allOptions = $attribute->getSource()->getAllOptions(true, true);  
foreach ($allOptions as $instance) {  
 $myArray[$instance[‘value’]] = $instance[‘label’];  
}  
Mage::log($myArray);{{< /highlight >}}

You will get list of all colors in an array called “myArray” in value => label format.