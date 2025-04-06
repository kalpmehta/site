---
id: 749
title: 'Magento get store information'
date: '2013-06-29T21:24:28+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=749'
permalink: /index.php/2013/06/29/magento-get-store-information/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2013/05/22/magento-recoverable-error-argument-1-passed-to/"     class="crp_title">Magento Recoverable Error Argument 1 passed to Mage_Core_Model_Store::setWebsite() must be an instance of&hellip;</a></li><li><a href="http://ka.lpe.sh/2012/10/16/magento-get-details-of-all-admin-users/"     class="crp_title">Magento: Get details of all Admin users</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
    - store
---

Magento get store information from any page.

{{< highlight php "style=emacs" >}}$store = Mage::app()->getStore(); //Mage_Core_Model_Store object{{< /highlight >}}

Now to get store ID,  
{{< highlight php "style=emacs" >}}$storeID = $store->getStoreId();{{< /highlight >}}

To get store code,  
{{< highlight php "style=emacs" >}}$storeCode = $store->getCode();{{< /highlight >}}

To get store Website ID,  
{{< highlight php "style=emacs" >}}$websiteID = $store->getWebsiteId();{{< /highlight >}}

To get store name,  
{{< highlight php "style=emacs" >}}$storeName = $store->getName();{{< /highlight >}}

To get Default View store name,  
{{< highlight php "style=emacs" >}}$storeName = $store->getFrontendName();{{< /highlight >}}

To check if store is active or not,  
{{< highlight php "style=emacs" >}}$active = $store->getIsActive();{{< /highlight >}}

To get store’s Home URL,  
{{< highlight php "style=emacs" >}}$storeHomeURL = $store->getHomeUrl();{{< /highlight >}}

If you want to find store’s group name,  
{{< highlight php "style=emacs" >}}$storeGroupName = $store->getGroup()->getName();{{< /highlight >}}

If you want ADMIN Store information, admin store has ID 0. So, you can get the details of Admin Store like this:  
{{< highlight php "style=emacs" >}}$store = Mage::getModel(‘core/store’)->load(0);{{< /highlight >}}

and then getting all the information as shown above.