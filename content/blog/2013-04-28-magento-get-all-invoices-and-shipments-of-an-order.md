---
id: 538
title: 'Magento get all invoices and shipments of an order'
date: '2013-04-28T19:37:49+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=536'
permalink: /index.php/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2013/04/18/change-default-length-of-increment-id-for-orders-invoices-shipments-creditmemos/"     class="crp_title">Change default length of Increment ID for orders, invoices, shipments, creditmemos</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-get-all-latest-tracking-number-of-any-shipment/"     class="crp_title">Magento: Get all/latest tracking number of any shipment</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - invoice
    - magento
    - order
    - shipment
---

**Getting all the invoices of an order:**  
{{< highlight php "style=emacs" >}}$order = Mage::getModel(‘sales/order’)->load($orderID);  
if ($order->hasInvoices()) {  
 $invIncrementIDs = array();  
 foreach ($order->getInvoiceCollection() as $inv) {  
 $invIncrementIDs[] = $inv->getIncrementId();  
 //other invoice details…  
 } Mage::log($invIncrementIDs);  
}{{< /highlight >}}

**Getting all the shipments of an order:**  
{{< highlight php "style=emacs" >}}$order = Mage::getModel(‘sales/order’)->load($orderID);  
foreach($order->getShipmentsCollection() as $shipment)  
{  
 Mage::log($shipment->getData()); //get each shipment data here…  
}{{< /highlight >}}