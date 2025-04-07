---
id: 463
title: 'Magento 500 internal server error'
date: '2013-02-09T18:15:42+00:00'
author: kalpesh
layout: post
tags:
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