---
id: 895
title: 'Magento: Clear all caches from command line'
date: '2014-06-22T18:58:17+00:00'
author: kalpesh
layout: post
tags:
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