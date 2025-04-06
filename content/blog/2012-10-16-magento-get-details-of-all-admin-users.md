---
id: 346
title: 'Magento: Get details of all Admin users'
date: '2012-10-16T14:54:31+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=346'
permalink: /index.php/2012/10/16/magento-get-details-of-all-admin-users/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-reset-download-limit-for-downloadable-product-item-order/"     class="crp_title">Magento: Reset download limit for downloadable product item/order</a></li></ul></div>'
categories:
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