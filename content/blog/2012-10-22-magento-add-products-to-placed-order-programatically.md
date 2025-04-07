---
id: 380
title: 'Magento: Add products to placed order programatically'
date: '2012-10-22T16:00:53+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'add items to order'
    - 'add product to order placed'
    - 'add products programatically to order'
    - 'edit order in magento'
    - 'magento attach products to order'
---

Ever wondered how to attach products to order programatically? It may require if you want to surprise your customer by giving them some special items along with their ordered products. Magento doesn’t allow you to do this, you need to write it through calling observer for event sales_order_place_after.

Copy this in the observer file which observes order place after event.  
{{< highlight php "style=emacs" >}}$product = Mage::getModel(‘catalog/product’)->loadByAttribute(‘sku’, $skuToAdd); //your product SKU to add  
$qty = 1;  
$rowTotal = $product->getPrice();  
$orderItem = Mage::getModel(‘sales/order_item’)  
 ->setStoreId($order->getStore()->getStoreId())  
 ->setQuoteItemId(NULL)  
 ->setQuoteParentItemId(NULL)  
 ->setProductId($product->getId())  
 ->setProductType($product->getTypeId())  
 ->setQtyBackordered(NULL)  
 ->setTotalQtyOrdered($qty)  
 ->setQtyOrdered($qty)  
 ->setName($product->getName())  
 ->setSku($product->getSku())  
 ->setPrice($product->getPrice())  
 ->setBasePrice($product->getPrice())  
 ->setOriginalPrice($product->getPrice())  
 ->setRowTotal($rowTotal)  
 ->setBaseRowTotal($rowTotal)  
 ->setOrder($order);  
$orderItem->save();{{< /highlight >}}  
Please note that you may also need to add the entry in sales_flat_quote_item table to be 100% sure it’s going to work for reorder also. If you’re not worried about reordering, the above code is fine.