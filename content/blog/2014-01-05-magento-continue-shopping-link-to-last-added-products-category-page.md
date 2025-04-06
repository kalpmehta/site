---
id: 863
title: "Magento continue shopping link to last added product's category page"
date: '2014-01-05T16:35:54+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=863'
permalink: /index.php/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/
snapEdIT:
    - '1'
snapFB:
    - 's:193:"a:1:{i:0;a:5:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li></ul></div>'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"419870006160420864";s:5:"pDate";s:19:"2014-01-05 16:36:25";}}";'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - 'category page'
    - 'continue shopping'
    - magento
---

In Magento checkout cart, link Continue shopping button to last added product’s category page. Below code will check last added product’s id in cart and gets the last category assigned to the product.

Put below code at the start of the checkout/cart.phtml file  
{{< highlight php "style=emacs" >}}$lastProductIdAddedToCart = Mage::getSingleton(‘checkout/session’)->getLastAddedProductId();  
if($lastProductIdAddedToCart) {  
 $productCategoryIdsArray = Mage::getModel(‘catalog/product’)->load($lastProductIdAddedToCart)->getCategoryIds();  
 //print_r($productCategoryIdsArray);  
 $continueShoppingCategoryUrl = Mage::getModel(‘catalog/category’)->load(end($productCategoryIdsArray))->getUrl();  
}{{< /highlight >}}

Replace continue shopping button with below code, in the checkout/cart.phtml file  
{{< highlight php "style=emacs" >}} <?php if($this->getContinueShoppingUrl()): ?>  
 <button title="<?php echo $this->__(‘Continue Shopping’) ?>” class=”button btn-continue” onclick=”setLocation(‘<?php echo (isset($continueShoppingCategoryUrl)) ? $continueShoppingCategoryUrl : $this->getContinueShoppingUrl(); ?>’)”><span><span><?php echo $this->__(‘Continue Shopping’) ?></span></span></button><br />
<?php endif; ?> " type="button"></button>{{< /highlight >}}