---
id: 160
title: 'Magento: Register guest user to website if email provided'
date: '2011-12-31T13:03:10+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=160'
permalink: /index.php/2011/12/31/magento-register-guest-user-to-website-if-email-provided/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-add-admin-user-in-mysql/"     class="crp_title">Magento add admin user in MySQL</a></li></ul></div>'
snapEdIT:
    - '1'
snapFB:
    - 's:166:"a:1:{i:0;a:4:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";}}";'
snapLI:
    - 's:178:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:99:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";}}";'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - checkout
    - customer
    - guest
    - magento
    - register
---

If your Magento website have feature where guest user can place an order without registering themself in your site, you can add them as a customer in your database. It helps in grouping the orders w.r.t email address in backend sales order. The only condition is that he should provide his email address while placing an order, which is quite obvious.

So here is a snippet of code you can insert where you are asking user to enter his email address. Just check if the user is already not registered in your site.

{{< highlight php "style=emacs" >}}$e = $email; //provided by guest user

$store = Mage::app()->getStore();  
$websiteId = Mage::app()->getWebsite()->getId();

$customerObj = Mage::getModel(‘customer/customer’);  
$customerObj->website_id = $websiteId;  
$customerObj->setStore($store);

$prefix = “mag”;  
$pwd = uniqid($prefix);

$session = Mage::getSingleton(‘checkout/session’);  
$fname = $session->getFirstname();  
$lname = $session->getLastname();

$customerObj->setEmail($e);  
$customerObj->setFirstname(‘Guest’);  
$customerObj->setLastname(‘Guest’);  
$customerObj->setPassword($pwd);  
$customerObj->save();  
$customerObj->sendNewAccountEmail(‘confirmed’); //auto confirmed  
{{< /highlight >}}

UPDATE: It depends where you want to keep this functionality on your site. I have put it in saveShippingMethodAction() function of Mage/Checkout/controllers/OnepageController.php file after extending. Don’t forget, this code should only be run if customer is guest.