---
id: 132
title: 'Magento Admin &#8211; Forcing Invoice and Ship button together'
date: '2011-12-31T10:41:25+00:00'
author: kalpesh
layout: post
tags:
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