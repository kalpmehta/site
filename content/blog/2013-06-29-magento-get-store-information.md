---
id: 749
title: 'Magento get store information'
date: '2013-06-29T21:24:28+00:00'
author: kalpesh
layout: post
tags:
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