---
id: 305
title: 'Magento: Check if customer already exist or not'
date: '2012-07-26T18:54:12+00:00'
author: kalpesh
layout: post
tags:
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