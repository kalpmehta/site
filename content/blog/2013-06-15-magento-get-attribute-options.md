---
id: 729
title: 'Magento get attribute options'
date: '2013-06-15T21:19:28+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - attribute
    - magento
---

Get attribute options list i.e. label and value, if the attribute type is dropdown.

This post will show you how to get all the options of attribute with dropdown type in Magento. If your attribute has options, below code will give all the attribute options labels and values in an array format.

{{< highlight php "style=emacs" >}}$attribute = Mage::getSingleton(‘eav/config’)->getAttribute(‘catalog_product’, ‘shirt_size’); //change shirt_size to your attribute code  
if ($attribute->usesSource()) {  
 $options = $attribute->getSource()->getAllOptions(false);  
 foreach($options as $option) {  
 print_r($option);  
 }  
}{{< /highlight >}}

In the above code, first line will initialize the attribute. Then we are checking if the attribute is using source model or not, if using then get all the options of that attribute.

It will output this for attribute shirt_size:

{{< highlight plain "style=emacs" >}}Array  
(  
 [value] => 100  
 [label] => Small  
)  
Array  
(  
 [value] => 99  
 [label] => Medium  
)  
Array  
(  
 [value] => 98  
 [label] => Large  
){{< /highlight >}}

If you are here to get attribute option’s label from value OR get attribute option’s value from label, just check out this post: <http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/>