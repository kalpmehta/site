---
id: 722
title: 'Magento get attribute value'
date: '2013-06-15T20:49:33+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - attribute
    - magento
---

To get product attribute value in Magento is very common. You will need it everytime when dealing with catalog products in your development. Attributes have different types, which can be any of Text Field, Text Area, Date, Yes/No, Multiple Select, Dropdown, Price, Gallery, Media Image, Fixed Product Tax (as you can see in backend *Manage Attributes > New Attribute > Catalog Input Type for Store Owner*). To get the value for these different types of attributes there is no one straight line of code, you will need to use different code for getting values from plain attributes, while different code to get values from select and multiselect attributes.

Get attribute value for PLAIN TEXT, TEXTAREA or DATE type attribute:  
{{< highlight php "style=emacs" >}}$attribute_value = $product->getShirtSize(); //for shirt_size attribute{{< /highlight >}}

Get value from SELECT, MULTISELECT, DROPDOWN or YES/NO attributes:  
{{< highlight php "style=emacs" >}}$attribute_value = $product->getAttributeText($attribute_code);{{< /highlight >}}  
OR  
{{< highlight php "style=emacs" >}}$attribute_value = $product->getResource()->getAttribute($attribute_code)->getFrontend()->getValue($product);{{< /highlight >}}

Get value from PRICE attributes:  
{{< highlight php "style=emacs" >}}$attribute_value = $product->getNew_price(); //for attribute code “new_price”{{< /highlight >}}  
and in product list page,  
{{< highlight php "style=emacs" >}}$attribute_value = $product->getNewPrice();{{< /highlight >}}

Get attribute value by attribute code and productID WITHOUT loading whole product  
{{< highlight php "style=emacs" >}}$attribute_value = Mage::getResourceModel(‘catalog/product’)->getAttributeRawValue($product_id, $attribute_code, $store_id);{{< /highlight >}}