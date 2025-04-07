---
id: 527
title: 'Magento join EAV collection with Flat table'
date: '2013-04-28T15:26:29+00:00'
author: kalpesh
layout: post
tags:
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