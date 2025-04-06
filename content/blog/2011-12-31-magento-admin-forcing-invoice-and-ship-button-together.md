---
id: 132
title: 'Magento Admin &#8211; Forcing Invoice and Ship button together'
date: '2011-12-31T10:41:25+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=132'
permalink: /index.php/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - 'invoice and ship'
    - 'magento admin'
---

Ever wondered what if you want to do invoice and shipment with just one click in your website admin? Yes, Magento allows you to integrate both these in one step.

Edit your module’s config.xml and Observer.php for this to happen.

**config.xml** snippet:  
{{< highlight xml "style=emacs" >}}<events>  
 <sales_order_place_after>  
 <observers>  
 <namespace_module>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>doForceInvoiceWithShipment</method>  
 </namespace_module>  
 </observers>  
 </sales_order_place_after>  
</events>{{< /highlight >}}  
Every time a order is placed, frontend as well as backend, your observer method will be called which will force invoice and shipment to show in one button in Manage Orders for particular order at backend.

**Observer.php** snippet:  
{{< highlight php "style=emacs" >}}public function doForceInvoiceWithShipment($observer) {  
 $order = $observer->getOrder();  
 $orderId = $order->getIncrementId();  
 Mage::getModel(‘sales/order’)->loadByIncrementId($orderId)->setForcedDoShipmentWithInvoice(true)->save();  
}{{< /highlight >}}

Now you can place a order and check at backend under Sales->Orders clicking on latest order to see “Invoice &amp; Ship” button integrated rather than “Invoice” and “Ship” button separated.