---
id: 155
title: 'Magento: Getting back shopping cart items after order fails'
date: '2011-12-31T12:09:56+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=155'
permalink: /index.php/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/10/10/magento-get-checkout-cart-total-details-subtotal-grandtotal-discount-tax/"     class="crp_title">Magento: Get checkout cart total details | Subtotal/Grandtotal/Discount/Tax</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li></ul></div>'
snapEdIT:
    - '1'
snapFB:
    - 's:166:"a:1:{i:0;a:4:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";}}";'
snapLI:
    - 's:178:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:99:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";}}";'
categories:
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