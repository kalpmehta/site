---
id: 922
title: 'Magento get CMS page content without header/footer'
date: '2014-08-22T03:35:56+00:00'
author: kalpesh
layout: post
tags:
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