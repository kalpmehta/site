---
id: 672
title: 'jQuery redirect page, with javascript alternative'
date: '2013-05-29T11:31:29+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=672'
permalink: /index.php/2013/05/29/jquery-redirect-page-with-javascript-alternative/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-remove-index-php-from-url/"     class="crp_title">Magento remove index.php from URL</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li></ul></div>'
categories:
    - jQuery
tags:
    - jquery
    - redirect
---

![jQuery javascript framework](http://ka.lpe.sh/wp-content/uploads/2013/06/jquery-logo.png)jQuery redirect one page to another using the following code:  
{{< highlight js "style=emacs" >}}var your_url = ‘http://ka.lpe.sh/’; //change this to your url  
$(location).attr(‘href’,’your_url’);{{< /highlight >}}

Above code works to redirect page in jQuery, but javascript code is good alternative here.

Using javascript to redirect your page using below code, which is better than jQuery, will do the job:  
{{< highlight js "style=emacs" >}}window.location.replace(“http://ka.lpe.sh/”);{{< /highlight >}}

Another javascript approach which will mock as if the URL is being clicked to redirect is:  
{{< highlight js "style=emacs" >}}window.location.href = “http://ka.lpe.sh/”;{{< /highlight >}}

Even this will do the trick in javascript, which sets your URL in a window object and assigns it to anchor tag’s href attribute automatically:  
{{< highlight js "style=emacs" >}}window.location = “http://ka.lpe.sh/”;{{< /highlight >}}