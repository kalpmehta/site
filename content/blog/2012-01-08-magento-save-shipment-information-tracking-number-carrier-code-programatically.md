---
id: 182
title: 'Magento: Save shipment information of order programatically'
date: '2012-01-08T15:23:03+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=182'
permalink: /index.php/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-get-all-latest-tracking-number-of-any-shipment/"     class="crp_title">Magento: Get all/latest tracking number of any shipment</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li></ul></div>'
categories:
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