---
id: 642
title: 'Magento remove index.php from URL'
date: '2013-05-26T14:39:38+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=642'
permalink: /index.php/2013/05/26/magento-remove-index-php-from-url/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li></ul></div>'
categories:
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