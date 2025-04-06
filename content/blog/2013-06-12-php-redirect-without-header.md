---
id: 705
title: 'PHP redirect without header()'
date: '2013-06-12T19:19:54+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=705'
permalink: /index.php/2013/06/12/php-redirect-without-header/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/29/jquery-redirect-page-with-javascript-alternative/"     class="crp_title">jQuery redirect page, with javascript alternative</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2013/06/01/return-false-vs-preventdefault-javascript/"     class="crp_title">return false vs preventDefault in javascript</a></li><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-get-email-address-and-created-updated-expires-dates-of-domain-name/"     class="crp_title">Linux: Bash script to get email address and created/updated/expires dates of domain name</a></li><li><a href="http://ka.lpe.sh/2013/06/01/jquery-prototype-conflict/"     class="crp_title">jQuery Prototype conflict, resolve it using noconflict</a></li></ul></div>'
categories:
    - PHP
tags:
    - php
    - redirect
---

It’s very frustrating when you want to redirect from one page to another, and you get the error:

*Warning: Cannot modify header information – headers already sent by (output started at /some/filename.php:12) in /some/filename.php on line 99*

The problem is Headers are already sent, or in simple language the output is already sent to browser when your header() function is called. The best solution is not to pass headers (send html/output to browser) till the point header() function is fired.

Another way is to use output buffering. Without output buffering (the default), your HTML is sent to the browser in pieces as PHP processes through your script. With output buffering, your HTML is stored in a variable and sent to the browser as one piece at the end of your script. For using this method, you have to start your file with *ob_start();* so that output gets buffered.

But what if you don’t care whether the output is sent or not, you anyway want the redirect to work? This simple function will do the trick for you. It will check if headers are not sent, then it will call the PHP’s header function to redirect. But if the headers are sent, it will use Javascript to redirect to the URL you want.

{{< highlight php "style=emacs" >}}function redirect($url)  
{  
 if (!headers_sent())  
 {  
 header(‘Location: ‘.$url);  
 exit;  
 }  
 else  
 {  
 echo ‘<script type="text/javascript">';
        echo 'window.location.href="'.$url.'";';
        echo '</script>‘;  
 echo ‘<noscript>‘;  
 echo ‘<meta content="0;url='.$url.'" http-equiv="refresh"></meta>‘;  
 echo ‘</noscript>‘;  
 exit;  
 }  
}{{< /highlight >}}