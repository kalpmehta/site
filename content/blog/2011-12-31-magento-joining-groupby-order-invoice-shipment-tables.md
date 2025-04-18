---
id: 143
title: 'Magento: Joining/group by &#8211; order, invoice, shipment tables'
date: '2011-12-31T11:09:45+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'magento admin'
    - 'magento join table'
    - 'magento orm'
    - 'order invoice shipment'
    - 'pickup report'
---

Ever tried to join multiple tables in Magento? Joining and grouping tables is not that easy in Magento ORM than in simple MySql way we did for years.

Here is a piece of code where I was required to grab all the data from orders, invoices, shipments to generate reports for warehouse people to make their life easier.

{{< highlight php "style=emacs" >}}$collection = Mage::getResourceModel(‘sales/order_shipment_item_collection’);  
$collection->addFieldToSelect(‘section_id’);  
$collection->addFieldToSelect(‘shelf_id’);  
$collection->addFieldToSelect(‘rack_id’);  
$collection->addFieldToSelect(‘box_id’);  
//$collection->addFieldToSelect(‘GROUP_CONCAT(DISTINCT main_table.product_id SEPARATOR “,”)’,’product_ids’);

$collection->getSelect()->joinLeft(‘sales_flat_shipment_grid’, ‘main_table.parent_id = sales_flat_shipment_grid.entity_id’, array(‘increment_id as shipment_increment_id’, ‘created_at as shipment_created_at’, ‘order_increment_id’,’total_qty’));  
$collection->getSelect()->joinLeft(‘sales_flat_shipment_track’, ‘sales_flat_shipment_grid.entity_id = sales_flat_shipment_track.parent_id’, array(‘number as track_id’, ‘carrier_code as carrier_name’));  
$collection->getSelect()->joinLeft(‘sales_flat_order’, ‘sales_flat_shipment_track.order_id = sales_flat_order.entity_id’, array(‘created_at as order_created_at’,’grand_total as ord_grand_total’));  
$collection->getSelect()->joinLeft(‘sales_flat_order_item’, ‘main_table.order_item_id = sales_flat_order_item.item_id’, array(‘product_type’));  
$collection->getSelect()->joinLeft(‘sales_flat_order_payment’, ‘sales_flat_shipment_track.order_id = sales_flat_order_payment.parent_id’, array(‘method as payment_method’));  
$collection->getSelect()->joinLeft(‘sales_flat_order_address’, ‘sales_flat_shipment_track.order_id = sales_flat_order_address.parent_id’, array(‘firstname’,’lastname’,’street’,’city’,’postcode’,’region’,’telephone’));  
$collection->getSelect()->joinLeft(‘sales_flat_invoice’, ‘sales_flat_shipment_track.order_id = sales_flat_invoice.order_id’, array(‘grand_total’));  
//$collection->addAttributeToFilter(‘main_table.price’, array(‘gt’ => 0));  
if($pickup_ids!=” &amp;&amp; is_array($pickup_ids))  
 $collection->addAttributeToFilter(‘sales_flat_shipment_grid.entity_id’, array(‘in’ => $pickup_ids));  
$collection->getSelect()->columns(  
 array(‘product_ids’ => new Zend_Db_Expr(  
 “IFNULL(GROUP_CONCAT(DISTINCT main_table.product_id SEPARATOR ‘;’), ”)”  
)));  
$collection->getSelect()->columns(  
 array(‘weight’ => new Zend_Db_Expr(  
 “IFNULL(SUM(main_table.weight)/2, ”)”  
)));  
$collection->getSelect()->group(‘shipment_increment_id’);  
//$collection->getSelect()->group(‘track_id’);  
//Mage::log($collection->getSelect()->__toString());  
$this->setCollection($collection);  
//$this->getCollection()->getSelect()->limit();{{< /highlight >}}

Although the query is so expensive, I have not yet tried to optimize it due to lack of time.