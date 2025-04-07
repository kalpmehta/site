---
id: 1023
title: 'Magento get all items in cart'
date: '2015-10-13T21:23:50+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - cart
    - items
    - magento
---

Magento get all the items currently in cart programatically using below code. You can place it anywhere you wish to get information, phtml or php file. Instead of **Mage::getSingleton(‘checkout/session’)->getQuote()** you can also use **Mage::getSingleton(‘checkout/cart’)->getQuote()** to get same results. If you want to see what all product information is retrieved you can use $product->getData() inside the foreach loop to display in array format.

{{< highlight php "style=emacs" >}}$cart = Mage::getSingleton(‘checkout/session’)->getQuote();  
//$cart->getAllItems() to get ALL items, parent as well as child, configurable as well as it’s simple associated item  
foreach ($cart->getAllVisibleItems() as $item) {  
 $product = $item->getProduct();  
 $name = $product->getName();  
 $sku = $product->getSku();  
}{{< /highlight >}}

If you want all the items in collection format, you can call below code instead:  
{{< highlight php "style=emacs" >}}$itemsCollection = Mage::getSingleton(‘checkout/cart’)->getQuote()->getItemsCollection();{{< /highlight >}}