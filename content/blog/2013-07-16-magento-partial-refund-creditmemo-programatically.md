---
id: 763
title: 'Magento partial refund creditmemo programatically'
date: '2013-07-16T12:54:24+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - creditmemo
    - magento
    - programatically
    - refund
---

Suppose you have a product which is out of stock or something and you want to refund that product line item from order programatically. The below code will create creditmemo/refund for the products with certain SKU if it finds it in the line items of the order.

{{< highlight php "style=emacs" >}}Mage::app(‘admin’); //You can create creditmemo in admin area only  
//You should have $orderID as order increment ID and $sku as product SKU you want to refund for.  
$order = Mage::getModel(‘sales/order’)->loadByIncrementId($orderID);  
$orderItem = $order->getItemsCollection()->getItemByColumnValue(‘sku’, $sku);  
$service = Mage::getModel(‘sales/service_order’, $order);  
$data = array(  
 ‘qtys’ => array(  
 $orderItem->getId() => 1 //qty to refund.. $orderItem->getQty()  
 )  
);  
$creditMemo = $service->prepareCreditmemo($data)->save();{{< /highlight >}}