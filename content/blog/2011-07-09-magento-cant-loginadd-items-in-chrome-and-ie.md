---
id: 102
title: 'Magento: Can&#8217;t login/add items in Chrome and IE'
date: '2011-07-09T10:13:08+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=102'
permalink: /index.php/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/21/magento-how-to-runset-cron-in-magento/"     class="crp_title">Magento: How to run/set cron in Magento</a></li><li><a href="http://ka.lpe.sh/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/"     class="crp_title">Magento 1.5: Cannot login to admin panel after fresh install</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-and-set-variables-in-session/"     class="crp_title">Magento: Get and set variables in session</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
    - 'Magento frontend'
tags:
    - cookie
    - error
    - magento
---

**Problem**: In Chrome and IE, user as well as admin are unable to login as well as add items to cart. In Firefox, everything works fine.

**Solution**: This is due to the cookie problem, not in browser but in Magento itself. In Magento, by default cookie’s lifetime is set to 3600 (1 hour). But if the end users computer time runs ahead of server’s time, cookies will not get set for magento frontend as well as backend. For example, end user’s computer time is 1 hour forward than server’s time, that means the cookie (holding user’s session id) will expire as soon as user logs in or tries to add an item.

To solve this, set cookie’s lifetime to 86400 (1 day) instead of 1 hour and everything will work as expected. You can also set cookie lifetime to 0, so that cookie will only expire when the user’s browser is closed.

Go to: Magento backend -> Sytem -> Configuration -> Web -> Session and Cookie Management  
Set cookie lifetime to 86400 and save. Everything will work as expected now.