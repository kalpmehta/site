---
id: 843
title: 'Magento Error: Fatal error: Call to a member function rewrite() on a non-object in Mage /Core /Controller /Varien /Front.php on line 165'
date: '2013-10-20T08:56:15+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento error'
tags:
    - 'magento error'
---

Magento Error: Fatal error: Call to a member function rewrite() on a non-object in /var/www/magento/app/code/core/Mage/Core/Controller/Varien/Front.php on line 165

While upgrading Magento from 1.7 to 1.8 version, this error generally appears and stops the site from loading.

We can get rid of this error simply by clearing the cache:  
{{< highlight http >}} rm -rf var/cache/*{{< /highlight >}}  
If you don’t have terminal access, clear all the contents of var/cache/ directory.

Further if you have memcached or other caching system installed, flush them as well.