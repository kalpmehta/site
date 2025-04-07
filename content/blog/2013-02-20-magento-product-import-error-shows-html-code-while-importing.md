---
id: 473
title: 'Magento: Product Import error &#8211; shows HTML code while importing'
date: '2013-02-20T15:07:57+00:00'
author: kalpesh
layout: post
tags:
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