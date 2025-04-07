---
id: 85
title: 'Magento: Checking customer/admin is logged in or not'
date: '2011-06-19T07:07:47+00:00'
author: kalpesh
layout: post
tags:
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