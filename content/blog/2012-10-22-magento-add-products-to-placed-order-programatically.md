---
id: 380
title: 'Magento: Add products to placed order programatically'
date: '2012-10-22T16:00:53+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=380'
permalink: /index.php/2012/10/22/magento-add-products-to-placed-order-programatically/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li></ul></div>'
categories:
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