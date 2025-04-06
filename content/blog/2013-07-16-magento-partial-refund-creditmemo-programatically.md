---
id: 763
title: 'Magento partial refund creditmemo programatically'
date: '2013-07-16T12:54:24+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=763'
permalink: /index.php/2013/07/16/magento-partial-refund-creditmemo-programatically/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-reset-download-limit-for-downloadable-product-item-order/"     class="crp_title">Magento: Reset download limit for downloadable product item/order</a></li><li><a href="http://ka.lpe.sh/2013/04/18/change-default-length-of-increment-id-for-orders-invoices-shipments-creditmemos/"     class="crp_title">Change default length of Increment ID for orders, invoices, shipments, creditmemos</a></li></ul></div>'
categories:
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