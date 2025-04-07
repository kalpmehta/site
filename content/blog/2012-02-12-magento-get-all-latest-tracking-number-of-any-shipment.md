---
id: 206
title: 'Magento: Get all/latest tracking number of any shipment'
date: '2012-02-12T06:36:42+00:00'
author: kalpesh
layout: post
tags:
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