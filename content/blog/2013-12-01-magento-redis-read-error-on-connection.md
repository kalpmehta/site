---
id: 854
title: 'Magento Redis read error on connection'
date: '2013-12-01T19:57:02+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=854'
permalink: /index.php/2013/12/01/magento-redis-read-error-on-connection/
snapEdIT:
    - '1'
snapFB:
    - 's:193:"a:1:{i:0;a:5:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"407236953802035200";s:5:"pDate";s:19:"2013-12-01 19:57:10";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/10/20/magento-fatal-error-call-to-a-member-function-rewrite-on-a-non-object-in/"     class="crp_title">Magento Error: Fatal error: Call to a member function rewrite() on a non-object in&hellip;</a></li><li><a href="http://ka.lpe.sh/2013/05/22/magento-recoverable-error-argument-1-passed-to/"     class="crp_title">Magento Recoverable Error Argument 1 passed to Mage_Core_Model_Store::setWebsite() must be an instance of&hellip;</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/"     class="crp_title">Magento 1.5: Cannot login to admin panel after fresh install</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
tags:
    - cache
    - error
    - magento
    - redis
---

Magento read error on connection when using Redis. If you are using Redis as cache in Magento and read timeout is not specified, you may get this error. Below is how it looks in the error report.

{{< highlight http >}} read error on connection

Trace:  
\#1 lib/Mage/Cache/Backend/Redis.php(210): Credis_Client->hGet(‘zc:k:0cd_FPC_DE…’, ‘d’)  
\#2 lib/Zend/Cache/Core.php(303): Mage_Cache_Backend_Redis->load(‘0cd_FPC_DESIGN_…’, false)  
\#3 lib/Varien/Cache/Core.php(158): Zend_Cache_Core->load(‘FPC_DESIGN_EXCE…’, false, false)  
\#4 app/code/core/Mage/Core/Model/Cache.php(379): Varien_Cache_Core->load(‘FPC_DESIGN_EXCE…’)  
\#5 app/code/core/Enterprise/PageCache/Model/Processor.php(185): Mage_Core_Model_Cache->load(‘FPC_DESIGN_EXCE…’)  
\#6 app/code/core/Enterprise/PageCache/Model/Processor.php(146): Enterprise_PageCache_Model_Processor->_getDesignPackage()  
\#7 app/code/core/Enterprise/PageCache/Model/Processor.php(108): Enterprise_PageCache_Model_Processor->_createRequestIds()  
\#8 app/code/core/Mage/Core/Model/Cache.php(703): Enterprise_PageCache_Model_Processor->__construct()  
\#9 app/code/core/Mage/Core/Model/Cache.php(685): Mage_Core_Model_Cache->_getProcessor(‘Enterprise_Page…’)  
\#10 app/code/core/Mage/Core/Model/App.php(340): Mage_Core_Model_Cache->processRequest()  
\#11 app/Mage.php(683): Mage_Core_Model_App->run(Array)  
\#12 /var/www/source/index.php(87): Mage::run(”, ‘store’){{< /highlight >}}

The solution (atleast for us) was to add a read_timeout config option in app/etc/local.xml where you have configured Redis cache for Magento.

{{< highlight http >}} <cache>  
 <backend>Mage_Cache_Backend_Redis</backend>  
 <backend_options>  
 <server>127.0.0.1</server> <port>6379</port> <persistent></persistent> <database>0</database> <password></password> <force_standalone>0</force_standalone>  
 <connect_retries>1</connect_retries>  
 <read_timeout>10</read_timeout> <lifetimelimit>57600</lifetimelimit> <compress_data>0</compress_data>  
 </backend_options>  
</cache>{{< /highlight >}}

HTH!