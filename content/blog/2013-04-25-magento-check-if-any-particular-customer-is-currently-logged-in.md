---
id: 522
title: 'Magento: Check if any particular customer is currently logged in'
date: '2013-04-25T14:08:51+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=522'
permalink: /index.php/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/"     class="crp_title">Magento join EAV collection with Flat table</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - activity
    - customer
    - 'logged in'
    - magento
    - visitor
---

Let’s say you want to check if any particular customer is currently logged in to your site or not. Or let’s check how many customers with their customer IDs and other activities are online on your store.

This little script will help you in finding all the currently active OR any particular customer(s) active in your store.

{{< highlight php "style=emacs" >}}require “app/Mage.php”;  
umask(0);  
Mage::app();

$collection = Mage::getModel(‘log/visitor_online’)->prepare()->getCollection();

//Get all the customers that are logged in……  
foreach($collection->getData() as $cust) {  
 echo ‘Customer ID: ‘.$cust[‘customer_id’] . ‘  
‘;  
 echo ‘Last URL visited: ‘.$cust[‘last_url’] . ‘  
‘;  
 echo ‘First visit: ‘.$cust[‘first_visit_at’] . ‘  
‘;  
 echo ‘Last visit: ‘.$cust[‘last_visit_at’] . ‘  
‘;  
 echo ‘======================  
‘;  
}

//Get any particular customer, if he’s currently logged in or not…..  
$collection->addFieldToFilter(‘customer_id’, 5)->addCustomerData(); //5 is customer ID of customer you want to check  
if($collection->count()) {  
 echo ‘Customer is logged in’;  
} else {  
 echo ‘Customer is NOT logged in’;  
}{{< /highlight >}}