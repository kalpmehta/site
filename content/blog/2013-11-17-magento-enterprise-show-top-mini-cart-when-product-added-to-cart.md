---
id: 850
title: 'Magento enterprise: show top mini cart when product is added to cart'
date: '2013-11-17T11:40:23+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=850'
permalink: /index.php/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"402038546661658625";s:5:"pDate";s:19:"2013-11-17 11:40:33";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2011/10/10/magento-get-checkout-cart-total-details-subtotal-grandtotal-discount-tax/"     class="crp_title">Magento: Get checkout cart total details | Subtotal/Grandtotal/Discount/Tax</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/06/01/jquery-prototype-conflict/"     class="crp_title">jQuery Prototype conflict, resolve it using noconflict</a></li><li><a href="http://ka.lpe.sh/2013/05/29/jquery-redirect-page-with-javascript-alternative/"     class="crp_title">jQuery redirect page, with javascript alternative</a></li></ul></div>'
categories:
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