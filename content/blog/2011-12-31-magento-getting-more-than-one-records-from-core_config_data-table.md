---
id: 140
title: 'Magento: Getting more than one records from core_config_data table'
date: '2011-12-31T10:56:20+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=140'
permalink: /index.php/2011/12/31/magento-getting-more-than-one-records-from-core_config_data-table/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/"     class="crp_title">Magento join EAV collection with Flat table</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li></ul></div>'
categories:
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