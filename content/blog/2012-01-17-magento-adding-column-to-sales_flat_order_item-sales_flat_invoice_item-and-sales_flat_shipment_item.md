---
id: 184
title: 'Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item'
date: '2012-01-17T17:01:13+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=184'
permalink: /index.php/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - magento
    - sales_flat_invoice_item
    - sales_flat_order_item
    - sales_flat_shipment_item
---

Suppose you want to add column to some table before it gets save in Magento. Example, Magento doesn’t save regular price of product when an order is placed, it only saves the selling price. So if your product have some special price in it, then Magento only saves it’s special price when an order is placed, so there is no track of regular price of that product in order item table. Same it goes to invoice item and shipment item. When creating invoice and shipment, Magento doesn’t have any track on the regular price of invoiced item’s and shipment item’s regular price.

So here I show you how you will add a column “product_mrp” in each of 3 tables and update the information without firing any query!

First of all, make an installer script in your module that will alter these three tables and add column “product_mrp” or any of your choice.  
  
{{< highlight php "style=emacs" >}}<?php $installer = $this;

$installer->
startSetup();

$installer->run(”  
 ALTER TABLE sales_flat_order_item ADD COLUMN product_mrp DECIMAL(12,4) NULL;  
 ALTER TABLE sales_flat_invoice_item ADD COLUMN product_mrp DECIMAL(12,4) NULL;  
 ALTER TABLE sales_flat_shipment_item ADD COLUMN product_mrp DECIMAL(12,4) NULL;  
“);

$installer->endSetup();

?>{{< /highlight >}}

After this is executed, you will find your columns added at the end of your tables.  
Now we will catch the event before order is placed, before invoice is created and before shipment is saved.

**config.xml**  
{{< highlight xml "style=emacs" >}}<sales_order_place_before>  
 <observers>  
 <adding_product_mrp_order>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>saveProductMrpInOrder</method>  
 </adding_product_mrp_order>  
 </observers>  
 </sales_order_place_before>

 <sales_order_invoice_save_before>  
 <observers>  
 <adding_product_mrp_invoice>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>saveProductMrpInInvoice</method>  
 </adding_product_mrp_invoice>  
 </observers>  
 </sales_order_invoice_save_before>

 <sales_order_shipment_save_before>  
 <observers>  
 <adding_product_mrp_shipment>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>saveProductMrpInShipment</method>  
 </adding_product_mrp_shipment>  
 </observers>  
 </sales_order_shipment_save_before>{{< /highlight >}}

Now comes the Observer part that will add our column data before data is actually saved in table.

**Observer.php**  
{{< highlight php "style=emacs" >}}public function saveProductMrpInOrder(Varien_Event_Observer $observer) {  
 $order = $observer->getEvent()->getOrder();  
 foreach($order->getAllItems() as $item) {  
 $price = Mage::getModel(‘catalog/product’)->load($item->getId())->getPrice();  
 $item->setProductMrp($price);  
 }  
 return $this;  
 }

 public function saveProductMrpInInvoice(Varien_Event_Observer $observer) {  
 $invoice = $observer->getEvent()->getInvoice();  
 foreach($invoice->getAllItems() as $item) {  
 $price = Mage::getModel(‘catalog/product’)->load($item->getProductId())->getPrice();  
 $item->setProductMrp($price);  
 }  
 return $this;  
 }

 public function saveProductMrpInShipment(Varien_Event_Observer $observer)  
 {  
 $shipment = $observer->getEvent()->getShipment();  
 foreach($shipment->getAllItems() as $item) {  
 $product = Mage::getModel(‘catalog/product’)->load($item->getProductId());  
 $price = $product->getPrice();  
 $item->product_mrp = $price;  
 }  
 }{{< /highlight >}}

Now clear the cache, and place order and create it’s invoice and shipment. You will find the regular price of each of your products in all these three useful tables and hence you can track the original price information even if your product’s price has been changed afterwards.

Happy coding!