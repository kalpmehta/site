---
id: 305
title: 'Magento: Check if customer already exist or not'
date: '2012-07-26T18:54:12+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=305'
permalink: /index.php/2012/07/26/magento-check-if-customer-already-exist-or-not/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/"     class="crp_title">Magento: Add customer Facebook, Twitter, Google+, Pinterest handles</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - 'check customer registered'
    - 'check email exist'
    - 'magento check user exists'
---

When trying to add new user programatically, you will need to first check whether the customer is already registered or not in the system. For that, email address is required, as Magento uses email address for login purposes.

Below is the code which checks if customer is already there in the database, with some particular website id if any.  
{{< highlight php "style=emacs" >}}protected function _customerExists($email, $websiteId = null)  
{  
 $customer = Mage::getModel(‘customer/customer’);  
 if ($websiteId) {  
 $customer->setWebsiteId($websiteId);  
 }  
 $customer->loadByEmail($email);  
 if ($customer->getId()) {  
 return $customer;  
 }  
 return false;  
}{{< /highlight >}}