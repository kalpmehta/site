---
id: 591
title: 'Magento get products by attribute set id or name'
date: '2013-05-10T19:18:29+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=591'
permalink: /index.php/2013/05/10/magento-get-products-by-attribute-set/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/"     class="crp_title">Magento: Get all the values of a Magento EAV for a particular attribute code</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-reset-download-limit-for-downloadable-product-item-order/"     class="crp_title">Magento: Reset download limit for downloadable product item/order</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - 'attribute set'
    - magento
    - product
---

In Magento get all the products by specific attribute set ID or Name with below code snippet. If you want to get products by attribute set Name, then first get the attribute set ID from name as shown in the first 4 lines of code. If you already have attribute set ID, ignore first 4 lines of code as it is only used if you have attribute set Name and not it’s ID.

The resultant array will give you all the products with all the attributes and values. You can narrow the attributes that you only need by specifying them when you call *$products->addAttributeToSelect(*)* or when you get all data from product *$prod->getData()*.

{{< highlight php "style=emacs" >}}//If planning to get all products by attribute set NAME  
$attrSetName = ‘your_attribute_set_name_here’;  
$attributeSetId = Mage::getModel(‘eav/entity_attribute_set’)  
 ->load($attrSetName, ‘attribute_set_name’)  
 ->getAttributeSetId();

//If planning to get all products by attribute set ID  
$attributeSetId = ‘your_attribute_set_id_here’;

$products = Mage::getModel(‘catalog/product’)->getCollection();  
$products->addAttributeToFilter(‘attribute_set_id’,$attributeSetId);

$products->addAttributeToSelect(‘*’);

$products->load();  
foreach($products as $prod) {  
 $productsArray[] = $prod->getData(); //get all data or specify any attribute  
}

Mage::log($productsArray());{{< /highlight >}}