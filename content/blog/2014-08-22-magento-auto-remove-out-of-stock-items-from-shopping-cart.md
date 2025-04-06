---
id: 924
title: 'Magento auto remove out of stock items from shopping cart'
date: '2014-08-22T03:43:35+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=924'
permalink: /index.php/2014/08/22/magento-auto-remove-out-of-stock-items-from-shopping-cart/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2013/11/17/magento-enterprise-show-top-mini-cart-when-product-added-to-cart/"     class="crp_title">Magento enterprise: show top mini cart when product is added to cart</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-continue-shopping-link-to-last-added-products-category-page/"     class="crp_title">Magento continue shopping link to last added product&#8217;s category page</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - 'auto remove'
    - cart
    - magento
    - 'out of stock'
---

Magento automatically remove product items from shopping cart page which are out of stock. You may need this feature when the situation aries where product goes out of stock and that particular product is already there in other customer’s cart who have not yet checked it out. With this script Magento will auto-check if all the items in the cart are available and in-stock before proceeding for checkout page.

In config.xml file:  
{{< highlight xml "style=emacs" >}}  
<events>  
 <controller_action_predispatch_checkout_cart_index>  
 <observers>  
 <namespace_module_autoremove_outofstock>  
 <type>singleton</type>  
 <class>namespace_module/observer</class>  
 <method>autoRemoveOutOfStockItems</method>  
 </namespace_module_autoremove_outofstock>  
 </observers>  
 </controller_action_predispatch_checkout_cart_index>  
</events>  
{{< /highlight >}}

In Observer.php file:  
{{< highlight php "style=emacs" >}}  
public function autoRemoveOutOfStockItems($observer) {  
 $quote = Mage::getModel(‘checkout/session’)->getQuote();  
 $cartItems = $quote->getAllItems();  
 foreach ($cartItems as $item)  
 {  
 //$productType = $item->getProduct()->getTypeId();  
 //if($productType!=’configurable’) {  
 $productId = $item->getProductId();  
 $product = Mage::getModel(‘catalog/product’)->load($productId);  
 $stockItem = $product->getStockItem();  
 if(!$stockItem->getIsInStock())  
 {  
 Mage::helper(‘checkout/cart’)->getCart()->removeItem($item->getId())->save();  
 }  
 //}  
 }

}  
{{< /highlight >}}