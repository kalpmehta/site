---
id: 85
title: 'Magento: Checking customer/admin is logged in or not'
date: '2011-06-19T07:07:47+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=85'
permalink: /index.php/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-and-set-variables-in-session/"     class="crp_title">Magento: Get and set variables in session</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - admin
    - magento
    - session
---

The most important part in magento development is to check whether customer is logged in or not in the system. So that you can show specific features and extra privileges to your customers. There are many things that are restricted to the guests, while members can see the special privilege things.

Also if the customer is not logged in, we can show a link like “Log in”; while for logged in customers, we can show link like “Log out”, “My account”, etc. This is already present in Magento, but we may want to add more features to our customers. So here is the code where you can check customer is logged in or not.

This will check whether the customer is logged in the magento system or not.

{{< highlight php "style=emacs" >}}$session=Mage::getSingleton(‘customer/session’, array(‘name’=>’frontend’) );

if ($session->isLoggedIn()) {  
 echo “Welcome, “.$session->getCustomer()->getName();  
} else {  
 echo “Not logged in”;  
}{{< /highlight >}}

This will check whether admin is logged in or not in a magento site.

{{< highlight php "style=emacs" >}}$adminsession = Mage::getSingleton(‘admin/session’, array(‘name’=>’adminhtml’));

if($adminsession->isLoggedIn()) {  
 echo “Welcome Admin”;  
} else {  
 echo “Not logged in”;  
}{{< /highlight >}}