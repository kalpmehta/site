---
id: 967
title: 'Magento: Get real IP address behind a proxy'
date: '2014-11-07T18:48:19+00:00'
author: kalpesh
layout: post
tags:
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