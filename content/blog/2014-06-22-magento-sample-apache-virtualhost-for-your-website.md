---
id: 902
title: 'Magento: Sample apache virtualhost for your website'
date: '2014-06-22T19:16:40+00:00'
author: kalpesh
layout: post
tags:
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