---
id: 843
title: 'Magento Error: Fatal error: Call to a member function rewrite() on a non-object in Mage /Core /Controller /Varien /Front.php on line 165'
date: '2013-10-20T08:56:15+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=843'
permalink: /index.php/2013/10/20/magento-fatal-error-call-to-a-member-function-rewrite-on-a-non-object-in/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/22/magento-recoverable-error-argument-1-passed-to/"     class="crp_title">Magento Recoverable Error Argument 1 passed to Mage_Core_Model_Store::setWebsite() must be an instance of&hellip;</a></li><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2013/06/20/how-to-install-orocrm/"     class="crp_title">OroCRM Installation guide</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-debug-xml-layout-config-files/"     class="crp_title">Magento debug XML (layout, config) files</a></li></ul></div>'
categories:
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