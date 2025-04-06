---
id: 893
title: 'Magento: Enable logs on API calls'
date: '2014-06-22T18:16:23+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=893'
permalink: /index.php/2014/06/22/magento-enable-logs-on-api-calls/
crp_related_posts_feed:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li><li><a href="http://ka.lpe.sh/2012/07/21/magento-how-to-runset-cron-in-magento/"     class="crp_title">Magento: How to run/set cron in Magento</a></li><li><a href="http://ka.lpe.sh/2014/06/22/magento-sample-local-xml-template/"     class="crp_title">Magento: Sample local.xml template</a></li><li><a href="http://ka.lpe.sh/2013/05/29/jquery-check-if-checkbox-is-checked/"     class="crp_title">jQuery check if checkbox is checked or not</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-redirect-from-observer/"     class="crp_title">Magento redirect from observer</a></li></ul><div class="crp_clear"></div></div>'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapEdIT:
    - '1'
snapLI:
    - 's:174:"a:1:{i:0;a:4:{s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:4:"doLI";i:0;}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2012/07/21/magento-how-to-runset-cron-in-magento/"     class="crp_title">Magento: How to run/set cron in Magento</a></li><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li><li><a href="http://ka.lpe.sh/2013/05/29/jquery-check-if-checkbox-is-checked/"     class="crp_title">jQuery check if checkbox is checked or not</a></li><li><a href="http://ka.lpe.sh/2012/04/18/magento-get-sentence-case-from-camel-case-string/"     class="crp_title">Magento: Get sentence case from camel case string</a></li></ul></div>'
categories:
    - Magento
tags:
    - api
    - call
    - log
    - magento
---

There is no setting to enable/disable API calls in Magento, but you can do so by modifying a file which handles all the API calls and logging the requests in a custom log file. This is useful when you know that there are many API calls being requested by third party applications to your website but not sure what is actually being called, how many times, and at what day and time.

With that said, open the file: app/code/core/Mage/Api/Model/Server/Handler/Abstract.php  
and find the function “call” which handles all the API calls. Scroll down the function and find the if block which says:

{{< highlight php "style=emacs" >}}if (method_exists($model, $method)) {  
 if (isset($methodInfo->arguments) &amp;&amp; ((string)$methodInfo->arguments) == ‘array’) {  
 return $model->$method((is_array($args) ? $args : array($args)));  
 } elseif (!is_array($args)) {  
 return $model->$method($args);  
 } else {  
 return call_user_func_array(array(&amp;$model, $method), $args);  
 }  
} else {  
 throw new Mage_Api_Exception(‘resource_path_not_callable’);  
}{{< /highlight >}}

and replace it with:

{{< highlight php "style=emacs" >}}if (method_exists($model, $method)) {  
 Mage::log($method, null, ‘api.log’); //logs the method  
 Mage::log($args, null, ‘api.log’); //logs the arguments  
 if (isset($methodInfo->arguments) &amp;&amp; ((string)$methodInfo->arguments) == ‘array’) {  
 return $model->$method((is_array($args) ? $args : array($args)));  
 } elseif (!is_array($args)) {  
 return $model->$method($args);  
 } else {  
 return call_user_func_array(array(&amp;$model, $method), $args);  
 }  
} else {  
 throw new Mage_Api_Exception(‘resource_path_not_callable’);  
}{{< /highlight >}}

Now you should have your var/log/api.log file filled with the “method” and “arguments” requested by third party systems on your server. This should help you in knowing what was requested and at what time in your new log file.