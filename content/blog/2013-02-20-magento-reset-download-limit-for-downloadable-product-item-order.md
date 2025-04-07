---
id: 470
title: 'Magento: Reset download limit for downloadable product item/order'
date: '2013-02-20T08:21:32+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'downloadable product item order reset'
    - 'magento reset download limit'
    - 'reset downloads order item'
---

In Magento, downloadable products are the products which can be downloaded and does not require any shipping. When customer purchases this type of products, they get certain download limits to download their purchased items. This can be set in Products page in admin under “Downloadable Products” tab. In many cases store owner only want to give certain amount of downloads, so customers can’t download beyond that limit. But it may happen that due to bad internet or some interrupts downloads can’t be successful and customer want to reset that limit. For doing this, there is no option in backend to reset the download limits for the downloadable product items or for an entire order, and unfortunately admin use to re-order to achieve this.

Here is the query which will reset download limits for an entire order.  
{{< highlight php "style=emacs" >}}$q = Mage::getModel(‘sales/order_item’)->getCollection()->addFieldToSelect(‘order_id’);  
$q->getSelect()->joinRight(‘downloadable_link_purchased_item as d’, ‘main_table.item_id = d.order_item_id’,  
 array(‘item_id’,’number_of_downloads_used’));  
$q->getSelect()->where(‘main_table.order_id = ‘. (int)$orderId);  
$q->load();

//echo $q->getSelect()->__toString();exit;

$items = $q->getColumnValues(‘item_id’);  
foreach($items as $id) {  
 Mage::getModel(‘downloadable/link_purchased_item’)->load($id)  
 ->setStatus(‘available’)->setNumberOfDownloadsUsed(0)->save();  
}{{< /highlight >}}

The raw SQL query for the above Magento Convention query is:  
UPDATE sales_flat_order_item s RIGHT JOIN downloadable_link_purchased_item d ON s.item_id = d.order_item_id SET d.number_of_downloads_used = 0 WHERE s.order_id = $orderId;  
  
Here is another query that will allow you to reset download limits for a particular item in an order  
{{< highlight php "style=emacs" >}}$q = Mage::getModel(‘sales/order_item’)->getCollection()->addFieldToSelect(‘order_id’);  
$q->getSelect()->joinRight(‘downloadable_link_purchased_item as d’, ‘main_table.item_id = d.order_item_id’,  
 array(‘item_id’,’number_of_downloads_used’));  
$q->getSelect()->where(‘main_table.order_id = ‘. (int)$orderId .’ AND main_table.item_id = ‘. (int)$orderItemId);  
$q->load();

//echo $q->getSelect()->__toString();exit;

$items = $q->getColumnValues(‘item_id’);  
foreach($items as $id) {  
 Mage::getModel(‘downloadable/link_purchased_item’)->load($id)  
 ->setStatus(‘available’)->setNumberOfDownloadsUsed(0)->save();  
}{{< /highlight >}}

The raw SQL query for the above Magento Convention query is:  
UPDATE sales_flat_order_item s RIGHT JOIN downloadable_link_purchased_item d ON s.item_id = d.order_item_id SET d.number_of_downloads_used = 0 WHERE s.order_id = $orderId AND s.item_id = $orderItemId;

HTH!