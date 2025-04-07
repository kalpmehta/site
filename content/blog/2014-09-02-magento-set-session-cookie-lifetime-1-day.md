---
id: 930
title: 'Magento set session cookie lifetime to 1 day'
date: '2014-09-02T17:28:16+00:00'
author: kalpesh
layout: post
tags:
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