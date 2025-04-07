---
id: 642
title: 'Magento remove index.php from URL'
date: '2013-05-26T14:39:38+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
---

In Magento remove index.php from URL using below steps. It will convert your URL from

*http://www.example.com/index.php/blah*

to

*http://www.example.com/blah*

1.) In Magento *Admin > System > Configuration > Web > Search Engine Optimization*, change the value of *Web Server Rewrites* to *Yes*

Make sure your web server rewrite module is enabled. If you are using apache as your web server on Linux, you can check it by going to */etc/apache2/mods-enabled/rewrite.load*, if rewrite.load is present there it means your rewrite module is enabled. If not, you will need to copy *rewrite.load* from */etc/apache2/mods-available/* and paste it at */etc/apache2/mods-enabled/* location. Then reload the apache by running *service apache2 reload*.

2.) Check the file permission of .htaccess, it should be present in Magento root directory and readable by server.