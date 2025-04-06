---
id: 268
title: 'Magento: Get rid of admin notifications pop-up'
date: '2012-07-12T14:06:36+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=268'
permalink: /index.php/2012/07/12/magento-get-rid-of-admin-notifications-pop-up/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/"     class="crp_title">Magento 1.5: Cannot login to admin panel after fresh install</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2011/07/10/magento-show-only-specific-attributes-in-layered-navigation/"     class="crp_title">Magento: Show only specific attributes in layered navigation</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li></ul></div>'
categories:
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