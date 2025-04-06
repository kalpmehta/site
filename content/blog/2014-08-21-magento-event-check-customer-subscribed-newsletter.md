---
id: 920
title: 'Magento event to check if customer have subscribed to newsletter'
date: '2014-08-21T21:07:38+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=920'
permalink: /index.php/2014/08/21/magento-event-check-customer-subscribed-newsletter/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/08/21/magento-event-observer-customer-registration-success/"     class="crp_title">Magento event observer for customer registration success</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - event
    - magento
    - newsletter
    - observer
    - subscribed
---

Check if the customer has subscribed to the newsletter from registration page or checkout page by using event observer. You may need to take some action programatically if customer subscribes to newsletter, below code will help you exactly in that.

Code to put in your config.xml  
{{< highlight xml "style=emacs" >}}  
<newsletter_subscriber_save_after>  
 <observers>  
 <namespace_module_model_observer>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>subscribedToNewsletter</method>  
 </namespace_module_model_observer>  
 </observers>  
</newsletter_subscriber_save_after>  
{{< /highlight >}}

Code to put in your Observer.php file  
{{< highlight php "style=emacs" >}}  
class Namespace_Module_Model_Observer {  
 public function subscribedToNewsletter(Varien_Event_Observer $observer)  
 {  
 $event = $observer->getEvent();  
 $subscriber = $event->getDataObject();  
 $data = $subscriber->getData();  
 $email = $data[‘subscriber_email’];

 $statusChange = $subscriber->getIsStatusChanged();  
 if ($data[‘subscriber_status’] == “1” &amp;&amp; $statusChange == true) {  
 //code to handle if customer is just subscribed…  
 }  
 }  
}  
{{< /highlight >}}