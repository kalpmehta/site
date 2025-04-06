---
id: 1023
title: 'Magento get all items in cart'
date: '2015-10-13T21:23:50+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1023'
permalink: /index.php/2015/10/13/magento-get-all-items-in-cart/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/"     class="crp_title">Magento auto remove out of stock items from shopping cart</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-reload-top-mini-cart-programatically/"     class="crp_title">Magento reload top mini cart programatically</a></li><li><a href="http://ka.lpe.sh/2015/03/28/magento-checkout-cart-500-error/"     class="crp_title">Magento bug &#8211; Checkout cart 500 error &#8211; Redirect loops</a></li><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li></ul></div>'
categories:
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