---
id: 850
title: 'Magento enterprise: show top mini cart when product is added to cart'
date: '2013-11-17T11:40:23+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - enterprise
    - magento
    - minicart
---

Magento Enterprise comes with a top header mini-cart, which displays all the items with their custom options added to cart, when you click on My Cart in the header. This is a good feature, but what if you want to show this mini-cart each time a product is added, without clicking on that link? I will show you here how to display your mini cart automatically when a product is added to cart.

Open your cartheader.php file, which is located at:  
*app/design/frontend/enterprise/YOUR_DESIGN/template/checkout/cart/cartheader.phtml*

In the last few lines of this file, you should find the below line in javascript:

{{< highlight js "style=emacs" >}}Enterprise.TopCart.initialize(‘topCartContent’);  
// Below can be used to show minicart after item added  
// Enterprise.TopCart.showCart(7);{{< /highlight >}}

Replace the last line, **//Enterprise.TopCart.showCart(7);** with the below lines:

{{< highlight js "style=emacs" >}}jQuery( document ).ready(function() {  
 if( jQuery(‘#messages_product_view’).children().length ){  
 if(jQuery(‘#messages_product_view’).children().children().attr(‘class’) == ‘success-msg’) {  
 if(jQuery(‘.success-msg ul li span’).text().indexOf(‘was added to your shopping cart’) > -1) {  
 Enterprise.TopCart.showCart(7);  
 }  
 }  
 }  
});{{< /highlight >}}

So whenever in the page, there will be an element with ID “#messages_product_view” and it has a children with class “success-msg” and it has a ul/li/span with text containing “was added to your shopping cart”, we will show the top mini-cart. This is only true when an product is added to shopping cart.

You can also show top mini-cart without this jquery hack, by making a new module in Magento and catch the event when product is added to cart. Then programmatically clicking the top mini cart to display it. But according to me this small piece of code is better than to create whole new Magento module.

HTH!