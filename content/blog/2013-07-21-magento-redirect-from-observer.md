---
id: 796
title: 'Magento redirect from observer'
date: '2013-07-21T14:11:11+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=796'
permalink: /index.php/2013/07/21/magento-redirect-from-observer/
snapEdIT:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"358952355217149953";s:5:"pDate";s:19:"2013-07-21 14:11:25";}}";'
snap_isAutoPosted:
    - '1'
snapFB:
    - 's:302:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200415982346395";s:5:"pDate";s:19:"2013-07-21 14:11:30";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li></ul></div>'
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li></ul></div>'
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2013/07/12/magento-convert-quote-item-to-order-item/"     class="crp_title">Magento convert quote item to order item</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li></ul></div>'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5764718073063931904&amp;type=U&amp;a=50Uv";s:5:"pDate";s:19:"2013-07-21 14:11:32";}}";'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
    - observer
    - redirect
---

Redirection in observer doesn’t work normally as it do in Blocks, templates and controllers. Also there is no standard code to redirect from observer that works in every situation.

You will need an argument to achieve redirect when using below code:  
{{< highlight php "style=emacs" >}}public function observingMethod(Varien_Event_Observer $observer)  
{  
 $observer->getRequest()->setParam(‘return_url’,$urlToRedirect);  
}{{< /highlight >}}  
Note that $observer object should have getRequest() method to make above code work. You may need to use $observer->getEvent()->getFront()->getRequest() otherwise, or simply var_dump/Mage::log $observer to get better idea what methods the object have.

Or you can use below code which is not recommended:  
{{< highlight php "style=emacs" >}}public function observingMethod() {  
 header(‘Location: ‘ . $urlToRedirect);  
 exit;  
}{{< /highlight >}}  
We don’t need any arguments using above method.

Another approach, again not recommended:  
{{< highlight php "style=emacs" >}}public function observingMethod(Varien_Event_Observer $observer)  
{  
 $response = $observer->getResponse();  
 //$response = Mage::app()->getFrontController()->getResponse();  
 $response->setRedirect($urlToRedirect);

 Mage::app()->getFrontController()->sendResponse();  
}{{< /highlight >}}