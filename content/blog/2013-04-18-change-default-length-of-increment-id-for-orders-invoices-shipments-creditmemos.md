---
id: 498
title: 'Change default length of Increment ID for orders, invoices, shipments, creditmemos'
date: '2013-04-18T19:46:28+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - 'increment id order invoice shipment creditmemo'
    - 'magento change increment id length'
    - 'reduce increase increment id length'
---

By default in Magento CE 1.6, the default Increment ID of orders, invoices, shipments and creditmemos is 9 characters. If you want to make it short or long due to some other application dependency or whatever you will have to change the value of *increment_pad_length* in *eav_entity_type* table.

For changing it with some setup script installer, this code will do the trick:  
{{< highlight php "style=emacs" >}}$entityType = Mage::getModel(‘eav/entity_type’)->loadByCode(‘order’); //invoice, shipment, creditmemo  
$entityType->setIncrementPadLength(12)->save(); //changing length to 12{{< /highlight >}}

For changing it directly in database table, execute this queries:  
{{< highlight mariadb "style=emacs" >}}UPDATE `eav_entity_type` SET `increment_pad_length`= 12 WHERE entity_type_code = ‘order’;  
UPDATE `eav_entity_type` SET `increment_pad_length`= 12 WHERE entity_type_code = ‘invoice’;  
UPDATE `eav_entity_type` SET `increment_pad_length`= 12 WHERE entity_type_code = ‘shipment’;  
UPDATE `eav_entity_type` SET `increment_pad_length`= 12 WHERE entity_type_code = ‘creditmemo’;{{< /highlight >}}