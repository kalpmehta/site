---
id: 930
title: 'Magento set session cookie lifetime to 1 day'
date: '2014-09-02T17:28:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=930'
permalink: /index.php/2014/09/02/magento-set-session-cookie-lifetime-1-day/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/"     class="crp_title">Magento auto remove out of stock items from shopping cart</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-reload-top-mini-cart-programatically/"     class="crp_title">Magento reload top mini cart programatically</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - cookie
    - magento
    - session
---

Is your Magento shopping cart kicking out all the items after 24 minutes? Are you frustrated because your customer’s cart items are getting flushed every few hours even though you have correct setting in Magento? Do you want to increase your shopping cart sessions to last for 1 day (or anything you wish)?

Here are the things to look for to increase/decrease Magento’s session cookie lifetime.

In your php.ini file:  
{{< highlight http >}} session.gc_maxlifetime 86400{{< /highlight >}}  
If you have not changed this, it should be by default 1440 i.e. 24 minutes. Change it to 86400 for one day session lifetime

In your Magento admin:  
{{< highlight http >}} System -> Configuration -> Checkout -> Shopping Cart  
Quote Lifetime (days) -> 1{{< /highlight >}}

{{< highlight http >}} System -> Configuration -> Web -> Session Cookie Management  
Cookie Lifetime -> 86400{{< /highlight >}}

Make sure to check if you are in correct website/store if using multi-website/multi-store Magento setup. You can change the scope by changing the website/store from the upper left Store Switcher drop down in System -> Configuration screen.

If you are changing php.ini value, make sure you reload apache to reflect the changes.