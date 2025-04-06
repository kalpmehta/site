---
id: 999
title: 'Magento bug Checkout cart 500 error Redirect loops'
date: '2015-03-28T23:52:11+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=999'
permalink: /index.php/2015/03/28/magento-checkout-cart-500-error/
crp_related_posts_feed:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/"     class="crp_title">Magento auto remove out of stock items from shopping cart</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-reload-top-mini-cart-programatically/"     class="crp_title">Magento reload top mini cart programatically</a></li></ul><div class="crp_clear"></div></div>'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/"     class="crp_title">Magento auto remove out of stock items from shopping cart</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-reload-top-mini-cart-programatically/"     class="crp_title">Magento reload top mini cart programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - '500 internal server error'
    - bug
    - magento
    - 'shopping cart'
---

Magento checkout cart gives 500 error and redirect loops when there is a shopping cart rule with Category condition.

I found a bug in Magento which redirects shopping cart indefinitely causing it 500 internal server error. This can be a serious bug as customer will not able to shop if this happens. I noticed this happens when there is a shopping cart rule which have Category in conditions of the rule.

If total quantity equals or greater than 1 for a subselection of items in cart matching ALL of these conditions:  
**Category** is 125

So for example you have a shopping cart rule where you want to give some discount or free product if at least one product is chosen from specific Category, this triggers the error in frontend shopping cart. Main reason here is **Category** condition. If you remove category condition then the error should go away. But if you want to keep the category condition and still want Magento to handle the shopping cart promotion rule, check the code changes below:

To solve this I copied below file to my local  
app/code/core/Mage/SalesRule/Model/Rule/Condition/Product/Combine.php

and edited the function validate:  
{{< highlight php "style=emacs" >}}/**  
 * Validate a condition with the checking of the child value  
 * @param Varien_Object $object  
 *  
 * @return bool  
 */  
 public function validate(Varien_Object $object)  
 {  
 /** @var Mage_Catalog_Model_Product $product */  
 $product = $object->getProduct();  
 if (!($product instanceof Mage_Catalog_Model_Product)) {  
 $product = Mage::getModel(‘catalog/product’)->load($object->getProductId());  
 }

 $valid = parent::validate($object);

 /* Kalpesh commented whole block, as it causes redirect loop and Segmentation fault in apache  
 if (!$valid &amp;&amp; $product->getTypeId() == Mage_Catalog_Model_Product_Type_Configurable::TYPE_CODE) {  
 $children = $object->getChildren();  
 //$valid = $children &amp;&amp; $this->validate($children[0]); //Kalpesh commented, issue….  
 }*/

 return $valid;  
 }{{< /highlight >}}

Hope this helps to some troubled souls!