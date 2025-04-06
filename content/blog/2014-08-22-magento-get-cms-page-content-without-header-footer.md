---
id: 922
title: 'Magento get CMS page content without header/footer'
date: '2014-08-22T03:35:56+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=922'
permalink: /index.php/2014/08/22/magento-get-cms-page-content-without-header-footer/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li><li><a href="http://ka.lpe.sh/2012/07/12/magento-image-resize-compression-reduces-quality-jpeg/"     class="crp_title">Magento: Image resize/compression reduces quality of JPEG</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-debug-xml-layout-config-files/"     class="crp_title">Magento debug XML (layout, config) files</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - cms
    - magento
    - page
    - script
---

Magento get CMS page content anywhere on the site without header and footer using below script. You may need to do this for displaying CMS page on part of the page, like popup or sidebar of the page without using header and footer of the CMS page that generally comes when loading the page from the CMS URL.

{{< highlight php "style=emacs" >}}  
$page = Mage::getModel(‘cms/page’);  
$page->setStoreId(Mage::app()->getStore()->getId());  
$page->load(‘CMS-IDENTIFIER-HERE’,’identifier’); //EDIT IN THIS LINE  
$helper = Mage::helper(‘cms’);  
$processor = $helper->getPageTemplateProcessor();  
echo $html = $processor->filter($page->getContent());  
{{< /highlight >}}