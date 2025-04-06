---
id: 527
title: 'Magento join EAV collection with Flat table'
date: '2013-04-28T15:26:29+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=527'
permalink: /index.php/2013/04/28/magento-join-eav-collection-with-flat-table/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-reset-download-limit-for-downloadable-product-item-order/"     class="crp_title">Magento: Reset download limit for downloadable product item/order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - EAV
    - 'flat table'
    - join
    - magento
    - order
---

Joining tables in Magento when it comes to EAV with Flat table is quite complicated. Consider you want to join sales_flat_order table with customer EAV tables to get Customer’s firstname and lastname, it becomes difficult as customer’s name comes from customer_entity_varchar table.

Below code will join sales order flat table with customer EAV to get customer’s full name in the collection along with all the order details.

{{< highlight php "style=emacs" >}}$coll = Mage::getModel(‘sales/order’)->getCollection();

$fn = Mage::getModel(‘eav/entity_attribute’)->loadByCode(‘1’, ‘firstname’);  
$ln = Mage::getModel(‘eav/entity_attribute’)->loadByCode(‘1’, ‘lastname’);

$coll->getSelect()  
 ->join(array(‘ce1’ => ‘customer_entity_varchar’), ‘ce1.entity_id=main_table.customer_id’, array(‘firstname’ => ‘value’))  
 ->where(‘ce1.attribute_id=’.$fn->getAttributeId())  
 ->join(array(‘ce2’ => ‘customer_entity_varchar’), ‘ce2.entity_id=main_table.customer_id’, array(‘lastname’ => ‘value’))  
 ->where(‘ce2.attribute_id=’.$ln->getAttributeId())  
 ->columns(new Zend_Db_Expr(“CONCAT(`ce1`.`value`, ‘ ‘,`ce2`.`value`) AS fullname”));

print_r($coll->getData());{{< /highlight >}}