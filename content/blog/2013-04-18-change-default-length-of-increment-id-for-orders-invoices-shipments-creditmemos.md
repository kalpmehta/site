---
id: 498
title: 'Change default length of Increment ID for orders, invoices, shipments, creditmemos'
date: '2013-04-18T19:46:28+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=498'
permalink: /index.php/2013/04/18/change-default-length-of-increment-id-for-orders-invoices-shipments-creditmemos/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li></ul></div>'
categories:
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