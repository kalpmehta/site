---
id: 863
title: "Magento continue shopping link to last added product's category page"
date: '2014-01-05T16:35:54+00:00'
author: kalpesh
layout: post
tags:
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