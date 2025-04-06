---
id: 88
title: 'Magento: Some important functions'
date: '2011-06-19T07:37:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=88'
permalink: /index.php/2011/06/19/magento-some-important-functions/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li></ul></div>'
categories:
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