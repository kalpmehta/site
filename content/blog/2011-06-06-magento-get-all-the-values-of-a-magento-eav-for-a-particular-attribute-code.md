---
id: 38
title: 'Magento: Get all the values of a Magento EAV for a particular attribute code'
date: '2011-06-06T10:12:18+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=38'
permalink: /index.php/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li></ul></div>'
categories:
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