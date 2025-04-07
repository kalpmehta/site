---
id: 160
title: 'Magento: Register guest user to website if email provided'
date: '2011-12-31T13:03:10+00:00'
author: kalpesh
layout: post
tags:
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