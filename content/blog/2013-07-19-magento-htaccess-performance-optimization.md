---
id: 777
title: 'Magento tweak .htaccess for performance optimization'
date: '2013-07-19T01:09:41+00:00'
author: kalpesh
layout: post
tags:
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