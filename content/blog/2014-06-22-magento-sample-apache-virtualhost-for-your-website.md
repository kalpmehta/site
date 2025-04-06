---
id: 902
title: 'Magento: Sample apache virtualhost for your website'
date: '2014-06-22T19:16:40+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=902'
permalink: /index.php/2014/06/22/magento-sample-apache-virtualhost-for-your-website/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:174:"a:1:{i:0;a:4:{s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:4:"doLI";i:0;}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/06/20/how-to-install-orocrm/"     class="crp_title">OroCRM Installation guide</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-remove-index-php-from-url/"     class="crp_title">Magento remove index.php from URL</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-delete-empty-categories-and-sub-categories/"     class="crp_title">Magento delete empty categories and sub-categories</a></li></ul></div>'
categories:
    - Apache
    - Linux
    - Magento
tags:
    - apache
    - linux
    - magento
    - virtualhost
---

Sample apache virtualhost to point to your magento directory and run your local website with specified URL.

{{< highlight http >}} <virtualhost>  
 ServerAdmin webmaster@dummy-host.example.com  
 DocumentRoot “/var/www/magento/”  
 ServerName loca.lho.st  
 ServerAlias loca.lho.st  
 ErrorLog “logs/error_log”  
 CustomLog “logs/access_log” common  
</virtualhost>{{< /highlight >}}

Add entry to /etc/hosts too:

{{< highlight http >}} 127.0.0.1 loca.lho.st{{< /highlight >}}

Restart apache (service httpd restart OR service apache2 restart) and point your browser location to:  
{{< highlight http >}} http://loca.lho.st{{< /highlight >}}  
and you will see the website running from your /var/www/magento directory.