---
id: 95
title: 'Magento: Get customer details : customer id, name, email'
date: '2011-06-19T08:55:13+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=95'
permalink: /index.php/2011/06/19/magento-get-customer-id-name-email/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/"     class="crp_title">Magento join EAV collection with Flat table</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - magento
---

Magento get the logged in customer details like customer id, name, email, etc. Check if customer is already logged in or not, if they are logged in then get all the data using customer session object and use it as per the requirement.

{{< highlight php "style=emacs" >}}if (Mage::getSingleton(‘customer/session’)->isLoggedIn()) {  
 $customer = Mage::getSingleton(‘customer/session’)->getCustomer();  
 $customerData = Mage::getModel(‘customer/customer’)->load($customer->getId())->getData();  
 Mage::log($customerData);  
}{{< /highlight >}}

Output:  
{{< highlight php "style=emacs" >}}Array  
(  
 [entity_id] => 1  
 [entity_type_id] => 1  
 [attribute_set_id] => 0  
 [website_id] => 1  
 [email] => john.doe@example.com  
 [group_id] => 1  
 [increment_id] => 000000001  
 [store_id] => 1  
 [created_at] => 2007-08-30 23:23:13  
 [updated_at] => 2008-08-08 12:28:24  
 [is_active] => 1  
 [firstname] => John  
 [lastname] => Doe  
 [password_hash] => 204948a4020ed1d0e4238db2277d5:eg  
 [prefix] =>  
 [middlename] =>  
 [suffix] =>  
 [taxvat] =>  
 [default_billing] => 274  
 [default_shipping] => 274  
){{< /highlight >}}

Getting customer details from the $customerData object:  
{{< highlight php "style=emacs" >}}$customerID = $customerData->getId(); //entity_id can be used as id  
$name = $customerData->getFirstname() . ‘ ‘ . $customerData->getLastname();  
$isActive = $customerData->getIsActive();  
$email = $customerData->getEmail();  
$incrId = $customerData->getIncrementId();{{< /highlight >}}

Similarly, we can get lastname, email, etc. ( [website_id] = getWebsiteId() )