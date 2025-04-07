---
id: 519
title: 'Magento Special price products page'
date: '2013-04-25T11:26:42+00:00'
author: kalpesh
layout: post
tags:
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