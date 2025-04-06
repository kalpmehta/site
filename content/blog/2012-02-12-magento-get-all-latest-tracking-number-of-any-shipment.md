---
id: 206
title: 'Magento: Get all/latest tracking number of any shipment'
date: '2012-02-12T06:36:42+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=206'
permalink: /index.php/2012/02/12/magento-get-all-latest-tracking-number-of-any-shipment/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - 'get all trackings'
    - 'get latest tracking number'
    - magento
    - 'shipment track numbers'
---

In magento, if you have more than one tracking number assigned for any particular shipment, we need to show the latest track number with details to the customer.

Here I will show you how to get all tracking numbers as well as only the latest tracking number for any shipment.

**Get all tracking numbers for shipment**  
{{< highlight php "style=emacs" >}}  
$trackings=Mage::getResourceModel(‘sales/order_shipment_track_collection’)->addAttributeToSelect(‘*’)->addAttributeToFilter(‘parent_id’,$shipment->getId());  
$allTrackingIds = $trackings->getAllIds();  
//Mage::log($allTrackingIds);  
{{< /highlight >}}  
  
**Get only the latest tracking number for shipment**  
{{< highlight php "style=emacs" >}}  
$trackings=Mage::getResourceModel(‘sales/order_shipment_track_collection’)->addAttributeToSelect(‘*’)->addAttributeToFilter(‘parent_id’,$shipment->getId());  
$trackings->getSelect()->order(‘entity_id desc’)->limit(1);

$trackData = $trackings->getData();  
$trackID = $trackData[0][‘entity_id’];  
//Mage::log($trackID);  
{{< /highlight >}}