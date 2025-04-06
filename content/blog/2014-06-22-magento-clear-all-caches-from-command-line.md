---
id: 895
title: 'Magento: Clear all caches from command line'
date: '2014-06-22T18:58:17+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=895'
permalink: /index.php/2014/06/22/magento-clear-all-caches-from-command-line/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:174:"a:1:{i:0;a:4:{s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:4:"doLI";i:0;}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/08/11/magento-how-to-remove-order/"     class="crp_title">Magento how to remove order</a></li><li><a href="http://ka.lpe.sh/2013/10/20/magento-fatal-error-call-to-a-member-function-rewrite-on-a-non-object-in/"     class="crp_title">Magento Error: Fatal error: Call to a member function rewrite() on a non-object in&hellip;</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2013/06/20/how-to-install-orocrm/"     class="crp_title">OroCRM Installation guide</a></li></ul></div>'
categories:
    - Linux
    - Magento
tags:
    - cache
    - magento
---

Magento clear all caches from command line, programatically from ssh. Clearing the caches is a must when you are making any configuration changes in your Magento website. Although you can always clear the cache from admin panel, sometimes for faster cleaning or unable to log into admin panel reason, it’s good to have a script which will clear all the caches in Magento.

Create a file in your Magento root and name it clearCache.php with the below code:  
{{< highlight php "style=emacs" >}}<?php echo "Start Cleaning all caches at ... " . date("Y-m-d H:i:s") . "\n\n";
ini_set("display_errors", 1);

require 'app/Mage.php';
Mage::app('admin')->
setUseSessionInUrl(false);  
Mage::getConfig()->init();

$types = Mage::app()->getCacheInstance()->getTypes();

try {  
 echo “Cleaning data cache… \\n”;  
 flush();  
 foreach ($types as $type => $data) {  
 echo “Removing $type … “;  
 echo Mage::app()->getCacheInstance()->clean($data[“tags”]) ? “Cache cleared!” : “There is some error!”;  
 echo “\\n”;  
 }  
} catch (exception $e) {  
 die(“[ERROR:” . $e->getMessage() . “]”);  
}

echo “\\n”;

try {  
 echo “Cleaning stored cache… “;  
 flush();  
 echo Mage::app()->getCacheInstance()->clean() ? “Cache cleared!” : “There is some error!”;  
 echo “\\n\\n”;  
} catch (exception $e) {  
 die(“[ERROR:” . $e->getMessage() . “]”);  
}  
?>{{< /highlight >}}  
Make sure all the double quotes comes good in copy pasting.

You can now run this script by the command “php -f clearCache.php” from your magento root location in terminal and this will start clearing all the caches for you! Once done, it will confirm by the message “Cache cleared!” or giving error message if it fails.