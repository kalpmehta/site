---
id: 88
title: 'Magento: Some important functions'
date: '2011-06-19T07:37:16+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - functions
    - magento
---

Here I will show you some important functions/methods in Magento that will make your development easy.

Get the path of your magento page.  
{{< highlight php "style=emacs" >}}echo $this->getUrl(‘mypage’);{{< /highlight >}}

Get the path of the image in your skin folder.  
{{< highlight php "style=emacs" >}}echo $this->getSkinUrl(‘images/yourimage.gif’);{{< /highlight >}}

Get the product link.  
{{< highlight php "style=emacs" >}}echo $this->getProductData()->getProductUrl();{{< /highlight >}}

Get the product name.  
{{< highlight php "style=emacs" >}}echo $this->htmlEscape($this->getProductData()->getName());{{< /highlight >}}

Call a static block in .phtml file.  
{{< highlight php "style=emacs" >}}echo $this->getLayout()->createBlock(‘cms/block’)->setBlockId(‘YOURBLOCKID’)->toHtml();{{< /highlight >}}

Get Image url of current category.  
{{< highlight php "style=emacs" >}}echo $this->getCurrentCategory()->getImageUrl();{{< /highlight >}}

Check whether the current category is Top category.  
{{< highlight php "style=emacs" >}}echo $this->IsTopCategory();{{< /highlight >}}

Get description of current category.  
{{< highlight php "style=emacs" >}}echo $this->getCurrentCategory()->getDescription();{{< /highlight >}}

Display products list page (list.phtml).  
{{< highlight php "style=emacs" >}}echo $this->getProductListHtml();{{< /highlight >}}

Display CMS block page.  
{{< highlight php "style=emacs" >}}echo $this->getCmsBlockHtml();{{< /highlight >}}  
  
Get current store id.  
{{< highlight php "style=emacs" >}}echo $storeId = Mage::app()->getStore()->getId();{{< /highlight >}}

Get current store name.  
{{< highlight php "style=emacs" >}}echo $storeName = Mage::app()->getStore()->getName();{{< /highlight >}}

Get current store code.  
{{< highlight php "style=emacs" >}}echo $storeCode = Mage::app()->getStore()->getCode();{{< /highlight >}}

Get website name.  
{{< highlight php "style=emacs" >}}echo $websiteName = Mage::app()->getWebsite()->getName();{{< /highlight >}}

Get session id.  
{{< highlight php "style=emacs" >}}echo $sessionId = Mage::getModel(‘core/session’)->getSessionId();{{< /highlight >}}

Get customer id.  
{{< highlight php "style=emacs" >}}echo $customerId = Mage::getModel(‘customer/session’)->getCustomerId();{{< /highlight >}}

Get guest id.  
{{< highlight php "style=emacs" >}}echo $vistitorId = Mage::getModel(‘core/session’)->getVisitorId();{{< /highlight >}}