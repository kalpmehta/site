---
id: 182
title: 'Magento: Save shipment information of order programatically'
date: '2012-01-08T15:23:03+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'assign awb number'
    - magento
    - 'magento admin'
    - 'save shipment'
    - 'save tracking info'
    - 'shipment save before'
---

After creating invoice and shipment, it is necessary to add tracking information to shipment. Here is how to write a observer which will invoke as shipment save method is called and save tracking information programatically.

**config.xml** – under global -> events node  
{{< highlight xml "style=emacs" >}}<sales_order_shipment_save_before>  
 <observers>  
 <namespace_modulename_ship_before>  
 <type>singleton</type>  
 <class>Namespace_Modulename_Model_Observer</class>  
 <method>salesOrderShipmentSaveBefore</method>  
 </namespace_modulename_ship_before>  
 </observers>  
 </sales_order_shipment_save_before>{{< /highlight >}}

**Observer.php** -> under Model directory of module  
{{< highlight php "style=emacs" >}}public function salesOrderShipmentSaveBefore($observer)  
 {  
 $shipment = $observer->getEvent()->getShipment();  
 $track = Mage::getModel(‘sales/order_shipment_track’)  
 ->setNumber(‘824343454454’) //tracking number / awb number  
 ->setCarrierCode(‘aramex’) //carrier code  
 ->setTitle(‘Aramex’); //carrier title  
 $shipment->addTrack($track);  
 }{{< /highlight >}}