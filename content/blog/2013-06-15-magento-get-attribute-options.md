---
id: 729
title: 'Magento get attribute options'
date: '2013-06-15T21:19:28+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=729'
permalink: /index.php/2013/06/15/magento-get-attribute-options/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-label/"     class="crp_title">Magento get attribute label</a></li><li><a href="http://ka.lpe.sh/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/"     class="crp_title">Magento: Get all the values of a Magento EAV for a particular attribute code</a></li><li><a href="http://ka.lpe.sh/2013/02/07/magento-add-product-custom-attribute-options-dynamically/"     class="crp_title">Magento: Add product custom attribute options dynamically</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-list-of-all-product-attributes/"     class="crp_title">Magento get list of all product attributes</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li></ul></div>'
categories:
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