---
id: 916
title: 'Magento check if customer registered in checkout page'
date: '2014-08-21T20:49:54+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - checkout
    - customer
    - event
    - magento
    - register
---

If you want to check if the customer is guest, registered or just register to the site when they place the order, below script will help you identify that in success.phtml file.

You can find success / order confirmation phtml file at:  
app/design/frontend/[package]/[theme]/template/checkout/success.phtml

Just at the end of this file put below lines of code:  
{{< highlight php "style=emacs" >}}  
<?php $order = Mage::getModel('sales/order')->
loadByIncrementId($this->getOrderId());  
$quoteId = $order->getQuoteId();  
$quote = Mage::getModel(‘sales/quote’)->load($quoteId);  
$method = $quote->getCheckoutMethod(true);  
$customer_email = $order->getCustomerEmail();  
if ($method == ‘register’){ ?>  
//code to handle if customer just registered to your site  
<?php } elseif($method == 'guest') {??>
  
//code to handle if customer is guest  
<?php } else { ??>
  
//code to handle for logged in customer  
<?php } ??>
  
{{< /highlight >}}

In the same file, success.phtml, you can request for order number, customer email, customer id, subtotal, grandtotal, order ID just created etc. like this:  
{{< highlight php "style=emacs" >}}  
$_customerId = Mage::getSingleton(‘customer/session’)->getCustomerId();  
$lastOrderId = Mage::getSingleton(‘checkout/session’)->getLastOrderId();  
$order = Mage::getSingleton(‘sales/order’);  
$order->load($lastOrderId);  
$_totalData =$order->getData();  
$_sub = $_totalData[‘subtotal’];  
$_orderEmail = $_totalData[‘customer_email’];  
$_orderNumber = $_totalData[‘increment_id’];  
{{< /highlight >}}