---
id: 967
title: 'Magento: Get real IP address behind a proxy'
date: '2014-11-07T18:48:19+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=967'
permalink: /index.php/2014/11/07/magento-real-ip-address-behind-proxy/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-get-email-address-and-created-updated-expires-dates-of-domain-name/"     class="crp_title">Linux: Bash script to get email address and created/updated/expires dates of domain name</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-delete-empty-categories-and-sub-categories/"     class="crp_title">Magento delete empty categories and sub-categories</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'ip address'
    - magento
    - proxy
---

Get real IP address if your server or customer is behind a proxy network. Magento have function Mage::helper(‘core/http’)->getRemoteAddr(); to get client IP address, but it gives proxy IP address instead of real IP if there is proxy network in between. Below code checks and returns both real IP and proxy IP address if it founds any.

{{< highlight php "style=emacs" >}}if (!empty($_SERVER[‘HTTP_CLIENT_IP’])) {  
 echo $_SERVER[‘HTTP_CLIENT_IP’];  
} else if (!empty($_SERVER[‘HTTP_X_FORWARDED_FOR’])) {  
 $ips = explode(‘,’, $_SERVER[‘HTTP_X_FORWARDED_FOR’]);  
 echo trim($ips[count($ips) – 1]); //real IP address behind proxy IP  
 // echo $_SERVER[‘REMOTE_ADDR’]; //proxy IP address  
} else {  
 echo $_SERVER[‘REMOTE_ADDR’]; //no proxy found  
}{{< /highlight >}}