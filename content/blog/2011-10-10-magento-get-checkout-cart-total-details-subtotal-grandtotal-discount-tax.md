---
id: 123
title: 'Magento: Get checkout cart total details | Subtotal /Grandtotal /Discount /Tax'
date: '2011-10-10T14:22:36+00:00'
author: kalpesh
layout: post
tags:
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