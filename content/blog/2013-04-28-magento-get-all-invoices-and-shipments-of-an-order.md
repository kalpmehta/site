---
id: 538
title: 'Magento get all invoices and shipments of an order'
date: '2013-04-28T19:37:49+00:00'
author: kalpesh
layout: post
tags:
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