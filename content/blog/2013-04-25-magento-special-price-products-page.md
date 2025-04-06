---
id: 519
title: 'Magento Special price products page'
date: '2013-04-25T11:26:42+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=519'
permalink: /index.php/2013/04/25/magento-special-price-products-page/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li></ul></div>'
snapEdIT:
    - '1'
snapFB:
    - 's:166:"a:1:{i:0;a:4:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";}}";'
snapLI:
    - 's:178:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:99:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";}}";'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'cms page'
    - magento
    - 'sale products'
    - 'special price'
---

Magento special price products page. We will be creating a new CMS page that will display all the Special or Sale products. We can make a product as a Special by filling it’s “Special From” and “Special To” price in “Prices” tab in Manage Products individual screen.

So let’s first create CMS Page, by going to CMS > Pages, which we will name it as “Specials”. In the Content tab of that Page, paste the below line of code:  
{{< highlight http >}} {{block type=”catalog/product_special” template=”catalog/product/list.phtml” column_count=”3″ num_products=”0″}}{{< /highlight >}}  
and save the page.

– Here we are saying Magento to display Product List template by looking at our new block type file, Catalog/Product/Block/Special.php. So let’s create this file, Special.php in local/Mage/Catalog/Product/Block/ directory. You will have to create this directory path if it’s not already there.

{{< highlight php "style=emacs" >}}<?php class Mage_Catalog_Block_Product_Special extends Mage_Catalog_Block_Product_List
{
    protected function _getProductCollection()
    {
        if (is_null($this->
_productCollection)) {  
 $categoryID = $this->getCategoryId();  
 if($categoryID)  
 {  
 $category = new Mage_Catalog_Model_Category();  
 $category->load($categoryID); // this is category id  
 $collection = $category->getProductCollection();  
 } else  
 {  
 $collection = Mage::getResourceModel(‘catalog/product_collection’);  
 }

 $todayDate = date(‘m/d/y’);  
 $tomorrow = mktime(0, 0, 0, date(‘m’), date(‘d’)+1, date(‘y’));  
 $tomorrowDate = date(‘m/d/y’, $tomorrow);

 Mage::getModel(‘catalog/layer’)->prepareProductCollection($collection);  
 $collection->addAttributeToSort(‘created_at’, ‘desc’);  
 $collection->addStoreFilter();

 $collection->addAttributeToFilter(‘special_from_date’, array(‘date’ => true, ‘to’ => $todayDate))  
 ->addAttributeToFilter(‘special_to_date’, array(‘or’=> array(  
 0 => array(‘date’ => true, ‘from’ => $tomorrowDate),  
 1 => array(‘is’ => new Zend_Db_Expr(‘null’)))  
 ), ‘left’);

 $numProducts = $this->getNumProducts() ? $this->getNumProducts() : 0;  
 $collection->setPage(1, $numProducts)->load();

 $this->_productCollection = $collection;  
 }  
 return $this->_productCollection;  
 }  
}  
{{< /highlight >}}