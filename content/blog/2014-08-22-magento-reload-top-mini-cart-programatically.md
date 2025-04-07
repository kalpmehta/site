---
id: 926
title: 'Magento reload top mini cart programatically'
date: '2014-08-22T04:08:20+00:00'
author: kalpesh
layout: post
tags:
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