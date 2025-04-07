---
id: 893
title: 'Magento: Enable logs on API calls'
date: '2014-06-22T18:16:23+00:00'
author: kalpesh
layout: post

tags:
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