---
id: 940
title: 'Magento: Show gift card details in admin order page'
date: '2014-09-23T20:13:07+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=940'
permalink: /index.php/2014/09/23/magento-show-gift-card-details-in-admin-order-page/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/01/05/magento-display-categories-subcategories/"     class="crp_title">Magento display categories and sub-categories</a></li><li><a href="http://ka.lpe.sh/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/"     class="crp_title">WordPress: Show total/aggregate ratings and reviews to your posts/pages</a></li><li><a href="http://ka.lpe.sh/2013/06/01/return-false-vs-preventdefault-javascript/"     class="crp_title">return false vs preventDefault in javascript</a></li><li><a href="http://ka.lpe.sh/2013/06/03/prototype-utility-methods/"     class="crp_title">Prototype Utility Methods &#8211; Commonly used prototypejs functions</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - giftcard
    - magento
    - 'magento admin'
---

Magento display gift card details (code and amount) in Order View page of admin panel. When customer uses gift card in their order Magento does not display gift card code and amount details in admin panel which makes it tough to know. Customer can pay partially through gift card which makes even tougher as Magento only shows payment information of other method and not gift card amount deductions.

Below code will show you an additional block in magento admin panel with Gift Card details. If gift card is not used in an order, the block will simply no shown.

Open the file app/design/adminhtml/default/default/template/sales/order/view/edit.phtml

Add the below lines of code anywhere you want the gift card block to appear. I have used it after Account Information block.

{{< highlight php "style=emacs" >}}<?php $cards = unserialize($_order->
getGiftCards());  
 if($cards!=” &amp;&amp; count($cards)>0) { ?>

<div class="box-left"><div class="entry-edit"><div class="entry-edit-head">#### <?php echo Mage::helper('sales')->
__(‘Gift Cards’) ?>

</div><div class="fieldset"><div class="hor-scroll"><?php foreach ($cards as $card) { ??>
| <label><?php echo Mage::helper('sales')-> __(‘Giftcard Code’) ?></label> | <div style="font-weight:bold"><?php echo $card['c'];??> </div> |
|---|---|
| <label><?php echo Mage::helper('sales')-> __(‘Giftcard Amount’) ?></label> | <div style="font-weight:bold"><?php echo $card['a'];??> </div> |
 <?php }??>


</div></div></div></div><?php }??>
{{< /highlight >}}