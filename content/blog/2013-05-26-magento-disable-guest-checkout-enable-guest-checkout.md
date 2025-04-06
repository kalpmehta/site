---
id: 660
title: 'Magento disable guest checkout / enable guest checkout'
date: '2013-05-26T17:42:39+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=660'
permalink: /index.php/2013/05/26/magento-disable-guest-checkout-enable-guest-checkout/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2011/10/10/magento-get-checkout-cart-total-details-subtotal-grandtotal-discount-tax/"     class="crp_title">Magento: Get checkout cart total details | Subtotal/Grandtotal/Discount/Tax</a></li><li><a href="http://ka.lpe.sh/2012/07/12/magento-get-rid-of-admin-notifications-pop-up/"     class="crp_title">Magento: Get rid of admin notifications pop-up</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li></ul></div>'
snapFB:
    - 's:166:"a:1:{i:0;a:4:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";}}";'
snapEdIT:
    - '1'
snapLI:
    - 's:178:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:99:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";}}";'
categories:
    - Magento
    - 'Magento admin'
tags:
    - checkout
    - guest
    - magento
---

By default the guest checkout in Magento is enabled and visitors can place an order without registering to the website. Some websites require mandatory login for placing orders, and this default feature should be turned off to disallow guest checkout.

To disable guest checkout, navigate to:

*System > Configuration > Sales section > Checkout > Checkout Options*  
Set *Allow Guest Checkout* to *No*

This will now disable any guest checkout in your site.  
To enable guest checkout, simply set the above dropdown option to *Yes*.