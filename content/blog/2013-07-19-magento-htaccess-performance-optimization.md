---
id: 777
title: 'Magento tweak .htaccess for performance optimization'
date: '2013-07-19T01:09:41+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=777'
permalink: /index.php/2013/07/19/magento-htaccess-performance-optimization/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-remove-index-php-from-url/"     class="crp_title">Magento remove index.php from URL</a></li><li><a href="http://ka.lpe.sh/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/"     class="crp_title">Magento: Add customer Facebook, Twitter, Google+, Pinterest handles</a></li><li><a href="http://ka.lpe.sh/2013/06/01/return-false-vs-preventdefault-javascript/"     class="crp_title">return false vs preventDefault in javascript</a></li><li><a href="http://ka.lpe.sh/2013/06/01/jquery-prototype-conflict/"     class="crp_title">jQuery Prototype conflict, resolve it using noconflict</a></li></ul></div>'
categories:
    - Magento
    - Performance
tags:
    - magento
    - performance
---

Tweak .htaccess for performance optimization in Magento. It will not sky rocket your website, but will show notable improvement. The default Magento .htaccess comes with performance optimization, but commented by default. I will show you here which lines to uncomment and improve the performance.

## Compressing web pages with mod_deflate

The mod_deflate module allows the Apache2 web service to compress files and deliver them to browser that can handle them. With mod_deflate you can compress HTML, text or XML files by upto 70% of their original sizes! Thus, saving you server traffic and speeding up page loads.

Check your .htaccess file for below code, I have removed hashes before few lines to uncomment them for performance.  
{{< highlight http >}} <ifmodule mod_deflate.c=""></ifmodule>

\############################################  
\## enable apache served files compression  
\## http://developer.yahoo.com/performance/rules.html#gzip

 # Insert filter on all content  
 SetOutputFilter DEFLATE  
 # Insert filter on selected content types only  
 AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript

 # Netscape 4.x has some problems…  
 BrowserMatch ^Mozilla/4 gzip-only-text/html

 # Netscape 4.06-4.08 have some more problems  
 BrowserMatch ^Mozilla/4\\.0[678] no-gzip

 # MSIE masquerades as Netscape, but it is fine  
 BrowserMatch \\bMSIE !no-gzip !gzip-only-text/html

 # Don’t compress images  
 SetEnvIfNoCase Request_URI \\.(?:gif|jpe?g|png)$ no-gzip dont-vary

 # Make sure proxies don’t deliver the wrong content  
 Header append Vary User-Agent env=!dont-vary

{{< /highlight >}}

## Enabling expires header with mod_expires

Make browser cache static files with Apache2’s mod_expires module.

{{< highlight http >}} <ifmodule mod_expires.c=""></ifmodule>

\############################################  
\## Add default Expires header  
\## http://developer.yahoo.com/performance/rules.html#expires

 ExpiresActive On  
 ExpiresDefault “access plus 1 year”

{{< /highlight >}}