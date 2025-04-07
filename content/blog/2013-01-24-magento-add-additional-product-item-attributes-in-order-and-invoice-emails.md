---
id: 441
title: 'Magento: Add additional product/item attributes in order and invoice emails'
date: '2013-01-24T16:29:24+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - attribute
    - email
    - invoice
    - magento
    - order
---

Recently I was working with a German client, who wanted to show additional product attribute options in the order and invoice emails due to stricter law for e-commerce in their country. Magento provides basic information in the default email templates, but each store has their unique requirement to show additional information.

I will show you how to add extra product attribute values, along with order item options and custom options in order emails and invoice emails.

Here is the code that should work for order and invoice emails to get additional PRODUCT ATTRIBUTES displayed:  
{{< highlight php "style=emacs" >}}$productId = $_item->getProduct()->getId(); //for order emails  
//$productId = $_item->getProductId(); //for invoice emails  
$product = Mage::getModel(‘catalog/product’)->load($productId);  
$attributes = $product->getAttributes();

//Get a list of all PRODUCT ATTRIBUTES you want to show in this array…  
$dispAttribs = array(‘hardrive’, ‘memory’, ‘processor’);

foreach ($attributes as $attribute) {  
 $attributeCode = $attribute->getAttributeCode();  
 if(!in_array($attributeCode, $dispAttribs)) continue;  
 $label = $attribute->getFrontend()->getLabel($product);  
 $value = $attribute->getFrontend()->getValue($product);  
 echo “  
**” . $label . “:** ” . $value;  
}{{< /highlight >}}  
  
For displaying CUSTOM OPTIONS and/or ITEM OPTIONS from the item, use this:  
{{< highlight php "style=emacs" >}}foreach($this->getItemOptions() as $opt) {  
 if(isset($opt[‘option_id’])) { //for CUSTOM OPTIONS  
 echo “**” . $opt[‘label’] . “:** “. $opt[‘option_value’] . “  
“;  
 } else { //for ITEM OPTIONS  
 echo “**” . $opt[‘label’] . “:** “. $opt[‘value’] . “  
“;  
 }  
}{{< /highlight >}}

For adding code to ORDER emails, the file where the code should go is:  
app/design/frontend/base/default/template/email/order/items/order/default.phtml

For adding code to INVOICE emails, the file where the code should go is:  
app/design/frontend/base/default/template/email/order/items/invoice/default.phtml

Instead of base/default, you can put it in your custom theme location which is obvious.