---
id: 854
title: 'Magento Redis read error on connection'
date: '2013-12-01T19:57:02+00:00'
author: kalpesh
layout: post
tags:
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