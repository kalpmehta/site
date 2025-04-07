---
id: 268
title: 'Magento: Get rid of admin notifications pop-up'
date: '2012-07-12T14:06:36+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'magento admin notification'
    - 'magento notifications popup'
---

Ever annoyed by the notification which pops up everytime you login to your Magento admin panel? Well, you can get rid of those bugging notifications without changing core.

Just disable the output of Mage_AdminNotification at:  
System -> Configuration -> Advanced -> Disable Modules Output

Now logout and login, you will now never see those unwanted notifications.

Cheers!