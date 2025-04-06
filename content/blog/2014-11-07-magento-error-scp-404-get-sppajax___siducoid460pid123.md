---
id: 965
title: 'Magento error: SCP 404: GET /spp/ajax/?___SID=Uco/?id=460&#038;pid=123'
date: '2014-11-07T17:51:49+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=965'
permalink: /index.php/2014/11/07/magento-error-scp-404-get-sppajax___siducoid460pid123/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/404-room-not-found-lol-d/"     class="crp_title">404 Room not found.. LOL :D</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/07/19/magento-products-not-showing-in-categories/"     class="crp_title">Magento products not showing in categories</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
    - 'Magento frontend'
tags:
    - '404 error'
    - magento
---

If you are using Magento extension Simple Configurable Product (SCP http://www.magentocommerce.com/magento-connect/simple-configurable-products.html), it gets dangerous sometimes when you have configured Special Prices or Tiered Pricing. It requests for prices via ajax after page is loaded. For some customers having old system and browser, this results in sending ___SID (session ID) along with GET request parameter, which causes double question mark in the URL.

Ideally, the ajax URL should be:  
{{< highlight plain >}} http://ma.gen.to/spp/ajax/co?id=460&amp;pid=123 {{< /highlight >}}

where it requests to module’s AjaxController and coAction() method, with parameters id (product ID) and pid (parent ID). This should go good without any issue.

{{< highlight plain >}} http://ma.gen.to/spp/ajax/?___SID=Uco/?id=460&amp;pid=123 {{< /highlight >}}

But, ___SID=U, which is used in the cache as a placeorder, also goes along with the parameters it creates a problem. As there are two “?” in the URL, Magento will try to see for AjaxController’s indexAction() because when you don’t have anything for action part in URL, it by defaults to indexAction of the controller.

The problem doesn’t end in just a 404 error in error log, this also DISPLAYS whole 404 page just below the product price in product page. So, customer will get confused as there is a big 404 page inside the product page and configurable attributes like size, color and quantity box are pushed down. This may result in low sales when it appears frequently.

The easiest way to fix this is to create an action indexAction() and check if you have ___SID as a parameter, then just ignore it.

Add the following code in your module’s AjaxController.php file, just above the coAction():

{{< highlight php "style=emacs" >}}
public function indexAction() {  
 $p = $this->getRequest()->getParam(‘___SID’);  
 if($p) { return ""; }  
}
{{< /highlight >}}

This will solve the weird 404 page that gets displayed in product page, but not the 404 error coming up in the logs. You need to remove ?___SID=U from the URL when it appears in the request to completely resolve the issue.