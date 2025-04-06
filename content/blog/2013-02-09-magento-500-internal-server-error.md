---
id: 463
title: 'Magento 500 internal server error'
date: '2013-02-09T18:15:42+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=463'
permalink: /index.php/2013/02/09/magento-500-internal-server-error/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-product-import-error-shows-html-code-while-importing/"     class="crp_title">Magento: Product Import error &#8211; shows HTML code while importing</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/04/18/pdo_mysql-extension-is-not-installed/"     class="crp_title">pdo_mysql extension is not installed</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
tags:
    - '500 internal server error'
    - magento
    - 'magento error'
---

[Resolved]: Magento 500 internal server error  
If you are getting “500 Internal Server Error” then the reason might be permissions issue or fatal error.

In Magento, you can check the errors occured in files:  
var/log/system.log  
var/log/exception.log

You can even allow the error to output to your browser by editing your Magento index.php with:  
error_reporting(E_ALL | E_STRICT);  
ini_set(‘display_errors’, 1);

Also, try this to solve the error:  
– Check the owner of your magento project. It should be the server (www-data for apache)  
chown -R www-data:www-data .

– Change the directory permissions to 755 and file permissions to 644 for your project  
find . -type d -exec chmod 0755 {} \\;  
find . -type f -exec chmod 0644 {} \\;  
chmod 550 pear  
chmod 550 mage  
chmod 755 -R var

– Check after upgrade do you have your .htaccess file inside Magento root