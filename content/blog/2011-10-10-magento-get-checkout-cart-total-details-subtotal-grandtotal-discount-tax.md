---
id: 123
title: 'Magento: Get checkout cart total details | Subtotal /Grandtotal /Discount /Tax'
date: '2011-10-10T14:22:36+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=123'
permalink: /index.php/2011/10/10/magento-get-checkout-cart-total-details-subtotal-grandtotal-discount-tax/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li><li><a href="http://ka.lpe.sh/2013/01/04/magento-certification-preparation-interview-questions-answers/"     class="crp_title">Magento Certification Preparation / Interview Questions Answers</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li></ul></div>'
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
    - discount
    - grandtotal
    - magento
    - subtotal
    - tax
    - totals
---

In Magento, if you want to get shopping cart totals details anywhere across the site, you can do so by following piece of code:

{{< highlight php "style=emacs" >}}$totalItemsInCart = Mage::helper(‘checkout/cart’)->getItemsCount(); //total items in cart  
$totals = Mage::getSingleton(‘checkout/session’)->getQuote()->getTotals(); //Total object  
$subtotal = round($totals[“subtotal”]->getValue()); //Subtotal value  
$grandtotal = round($totals[“grand_total”]->getValue()); //Grandtotal value  
if(isset($totals[‘discount’]) &amp;&amp; $totals[‘discount’]->getValue()) {  
 $discount = round($totals[‘discount’]->getValue()); //Discount value if applied  
} else {  
 $discount = ”;  
}  
if(isset($totals[‘tax’]) &amp;&amp; $totals[‘tax’]->getValue()) {  
 $tax = round($totals[‘tax’]->getValue()); //Tax value if present  
} else {  
 $tax = ”;  
}{{< /highlight >}}