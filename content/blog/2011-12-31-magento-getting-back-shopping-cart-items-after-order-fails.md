---
id: 155
title: 'Magento: Getting back shopping cart items after order fails'
date: '2011-12-31T12:09:56+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - checkout
    - magento
    - 'order fails'
    - 'preserve cart'
    - 'restore cart'
---

It’s very awkward if users place an order in your website and by chance the order fails, from end user side or some technical glitch, shopping cart becomes empty. User have to again add items in cart and go through the process which becomes tedious and may be changing their mind to shop.

So here’s a code that does the trick and preserves shopping cart content even if order gets failed.  
Open your file where you’re handling your order failure action in frontend. (generally **Mage/Checkout/controllers/OnepageController.php**)  
{{< highlight php "style=emacs" >}}public function failureAction()  
{  
 $lastQuoteId = $this->getOnepage()->getCheckout()->getLastQuoteId();  
 $lastOrderId = $this->getOnepage()->getCheckout()->getLastOrderId();

 if ($lastQuoteId &amp;&amp; $lastOrderId) {  
 $orderModel = Mage::getModel(‘sales/order’)->load($lastOrderId);  
 if($orderModel->canCancel()) {

 $quote = Mage::getModel(‘sales/quote’)->load($lastQuoteId);  
 $quote->setIsActive(true)->save();

 $orderModel->cancel();  
 $orderModel->setStatus(‘canceled’);  
 $orderModel->save();

 Mage::getSingleton(‘core/session’)->setFailureMsg(‘order_failed’);  
 Mage::getSingleton(‘checkout/session’)->setFirstTimeChk(‘0’);  
 $this->_redirect(‘kcheckout/index/payment’, array(“_forced_secure” => true));  
 return;  
 }  
 }  
 if (!$lastQuoteId || !$lastOrderId) {  
 $this->_redirect(‘checkout/cart’, array(“_forced_secure” => true));  
 return;  
 }

 $this->loadLayout();  
 $this->renderLayout();  
}{{< /highlight >}}

Be noted here that we don’t have here onepage checkout so we’re redirecting user to payment page after restoring the cart. You can redirect user to any page as per your need after the cart is restored and previous order is cancelled.