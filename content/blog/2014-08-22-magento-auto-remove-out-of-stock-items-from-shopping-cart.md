---
id: 924
title: 'Magento auto remove out of stock items from shopping cart'
date: '2014-08-22T03:43:35+00:00'
author: kalpesh
layout: post
tags:
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