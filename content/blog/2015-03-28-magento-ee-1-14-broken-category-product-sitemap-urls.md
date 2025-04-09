---
id: 991
title: 'Magento EE 1.14 &#8211; Broken category &#038; product sitemap URLs'
date: '2015-03-28T04:40:23+00:00'
author: kalpesh
layout: post

tags:
    - Magento
    - 'Magento admin'
tags:
    - bug
    - enterprise
    - magento
    - sitemap
---

Magento EE 1.14 introduces a bug fix which apparently becomes a bug in our website. [Magento EE 1.14.0.0 Release Notes](http://www.magentocommerce.com/knowledge-base/entry/ee114-later-release-notes#ee114-1400fixes-other) and [Magento CE 1.9.0.0 Release Notes](http://www.magentocommerce.com/knowledge-base/entry/ce19-later-release-notes#ce19-1900fixes-other) lists this in it’s Bug Fixes:  
*Google Sitemap files now include the .html suffix for category and product URLs.*

We don’t have .html suffix in our category and product URLs, so we were good before this fix. But after upgrading it to latest version all the category and product URLs were having “.” (dot) at the end in XML sitemap. This is because Magento allows admin to give a custom suffix for category and product URLs for sitemap, but hardcodes “.” regardless of there are values in the above config fields or not. This allows unnecessary dots in all the URLs which can lead to 404 pages.

[![Magento Category Product URL config](http://ka.lpe.sh/uploads/2015/03/Screen-Shot-2015-03-27-at-9.24.08-PM.png)](http://ka.lpe.sh/uploads/2015/03/Screen-Shot-2015-03-27-at-9.24.08-PM.png)

Magento team have used observer to observe the events *sitemap_categories_generating_before* and *sitemap_products_generating_before* to add the suffix in the following file and functions (Notice I have commented all lines in the functions):  
app/code/core/Enterprise/Catalog/Model/Observer.php  
(copy this file to app/code/local/Enterprise/Catalog/Model/Observer.php, you may have to create directories)  
{{< highlight php "style=emacs" >}}/**  
 * Add Seo suffix to category’s URL if doesn’t exists.  
 *  
 * @param Varien_Event_Observer $observer  
 */  
 public function addSeoSuffixToCategoryUrl(Varien_Event_Observer $observer)  
 {  
 /*$seoSuffix = (string) Mage::app()->getStore()->getConfig(  
 Mage_Catalog_Helper_Category::XML_PATH_CATEGORY_URL_SUFFIX  
 );  
 $this->_addSuffixToUrl($observer->getCollection()->getItems(), $seoSuffix);*/  
 }

 /**  
 * Add Seo suffix to product’s URL if doesn’t exists.  
 *  
 * @param Varien_Event_Observer $observer  
 */  
 public function addSeoSuffixToProductUrl(Varien_Event_Observer $observer)  
 {  
 /*$seoSuffix = (string) Mage::app()->getStore()->getConfig(  
 Mage_Catalog_Helper_Product::XML_PATH_PRODUCT_URL_SUFFIX  
 );  
 $this->_addSuffixToUrl($observer->getCollection()->getItems(), $seoSuffix);*/  
 }{{< /highlight >}}

After commenting above function’s logic and generating the Google Sitemap again (Admin > Catalog > Google Sitemap) everything was normal (no dot and suffix in URLs)