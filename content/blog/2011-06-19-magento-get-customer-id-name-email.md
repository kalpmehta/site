---
id: 95
title: 'Magento: Get customer details : customer id, name, email'
date: '2011-06-19T08:55:13+00:00'
author: kalpesh
layout: post
tags:
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