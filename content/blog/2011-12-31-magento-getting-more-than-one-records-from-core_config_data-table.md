---
id: 140
title: 'Magento: Getting more than one records from core_config_data table'
date: '2011-12-31T10:56:20+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - core_config_data
    - magento
---

To select any particular record from core_config_data table in magento is quite simple.  
{{< highlight php "style=emacs" >}}Mage::getStoreConfig(‘sales_email/order/template’);{{< /highlight >}}  
But what if you want all the data pertaining to sales order email or for any other thing stored in magento’s config table? You may need other data like “enabled”, “identity”, “guest_template”, “copy_to” which can accomplish otherwise in 5 requests.  
So here is how you should write the code to get all the data for some particular expression as per your need.  
{{< highlight php "style=emacs" >}}$qrySalesOrder = Mage::getModel(‘core/config_data’)->getCollection()->addFieldToFilter(‘path’,array(‘like’=>’sales_email/order/%’));  
//Mage::log($qrySalesOrder);{{< /highlight >}}