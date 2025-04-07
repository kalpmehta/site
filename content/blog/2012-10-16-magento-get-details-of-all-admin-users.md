---
id: 346
title: 'Magento: Get details of all Admin users'
date: '2012-10-16T14:54:31+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'get admin details'
    - 'magento get all admins'
---

As we can get details of all the customers of the Magento store, we can also get details of all the Admin users. It may be necessary sometimes when you want to display all the admin uses either in dropdown for filtering something or just as a text or something based on requirement.

The following code will get you all the Admin users with their details:  
{{< highlight php "style=emacs" >}}$adminUserModel = Mage::getModel(‘admin/user’);  
$userCollection = $adminUserModel->getCollection()->load();  
Mage::log($userCollection->getData());{{< /highlight >}}