---
id: 940
title: 'Magento: Show gift card details in admin order page'
date: '2014-09-23T20:13:07+00:00'
author: kalpesh
layout: post
tags:
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