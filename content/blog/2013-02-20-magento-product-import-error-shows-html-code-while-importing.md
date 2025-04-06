---
id: 473
title: 'Magento: Product Import error &#8211; shows HTML code while importing'
date: '2013-02-20T15:07:57+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=473'
permalink: /index.php/2013/02/20/magento-product-import-error-shows-html-code-while-importing/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2012/01/17/404-room-not-found-lol-d/"     class="crp_title">404 Room not found.. LOL :D</a></li><li><a href="http://ka.lpe.sh/2013/04/18/pdo_mysql-extension-is-not-installed/"     class="crp_title">pdo_mysql extension is not installed</a></li><li><a href="http://ka.lpe.sh/2012/11/02/buy-pinterest-autopost-images-right-from-your-website/"     class="crp_title">Buy: Pinterest AutoPost images right from your website!</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
tags:
    - 'magento error product import'
    - 'product import doctype html error'
---

While importing products (somewhere around 1200 rows) by Magento’s in-built “System > Import/Export > Dataflow – Profiles” I got an error where the Dashboard’s HTML was printed in the output.

![magento product import error](http://ka.lpe.sh/wp-content/uploads/2013/02/import_error.png)

The reason for this error is due to something wrong in CSV product data which Magento didn’t understand. Create a temporary CSV file with only few rows (2-4) and check if that works. If it works, that means there is some problem with rest of the data.

For more information check my SO question here: <http://stackoverflow.com/questions/14978970/magento-importing-product-error/14980974>