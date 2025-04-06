---
id: 918
title: 'Magento event observer for customer registration success'
date: '2014-08-21T21:00:10+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=918'
permalink: /index.php/2014/08/21/magento-event-observer-customer-registration-success/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/08/21/magento-check-customer-registered-checkout-page/"     class="crp_title">Magento check if customer registered in checkout page</a></li><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - event
    - magento
    - observer
    - register
---

If you are looking for how to execute some code when customer successfully sign up in your website, you can use below code to check if the registration was successful. Note, this will NOT check if customer was registered from checkout page, if you are looking for that please go to this [post](http://ka.lpe.sh/2014/08/21/magento-check-customer-registered-checkout-page/).

In your xml file:  
{{< highlight xml "style=emacs" >}}  
<events>  
 <customer_register_success>  
 <observers>  
 <namespace_module_customer_register_success>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>customerRegisterSuccess</method>  
 </namespace_module_customer_register_success>  
 </observers>  
 </customer_register_success>  
</events>  
{{< /highlight >}}

And in your Observer.php file:  
{{< highlight php "style=emacs" >}}  
class Namespace_Module_Model_Observer {  
 public function customerRegisterSuccess(Varien_Event_Observer $observer) {  
 $event = $observer->getEvent();  
 $customer = $event->getCustomer();  
 $email = $customer->getEmail();  
 if($email) {  
 //code to handle if customer is successfully registered  
 }  
 }  
}  
{{< /highlight >}}