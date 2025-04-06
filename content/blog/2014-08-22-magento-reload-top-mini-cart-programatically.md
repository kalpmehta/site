---
id: 926
title: 'Magento reload top mini cart programatically'
date: '2014-08-22T04:08:20+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=926'
permalink: /index.php/2014/08/22/magento-reload-top-mini-cart-programatically/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/"     class="crp_title">Magento auto remove out of stock items from shopping cart</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2011/10/10/magento-get-checkout-cart-total-details-subtotal-grandtotal-discount-tax/"     class="crp_title">Magento: Get checkout cart total details | Subtotal/Grandtotal/Discount/Tax</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - magento
    - 'mini cart'
    - reload
---

Magento reload/refresh top mini cart programatically. This can be useful when you are using ajax to add/remove product to cart and want to reflect that item changes in the top cart immediately. Simply put below code where you are modifying cart programatically and it will start working.

Right now it’s only coded for simple and configurable products, but you can add bundle, group, virtual and downloader product item renderers too if you are using them in your website.

{{< highlight php "style=emacs" >}}  
$b = $this->getLayout()  
->createBlock(‘checkout/cart_sidebar’)  
->addItemRender(‘simple’, ‘checkout/cart_item_renderer’, ‘checkout/cart/sidebar/default.phtml’)  
->addItemRender(‘configurable’, ‘checkout/cart_item_renderer_configurable’, ‘checkout/cart/sidebar/default.phtml’)  
->setTemplate(‘checkout/cart/cartheader.phtml’)  
->toHtml();  
{{< /highlight >}}