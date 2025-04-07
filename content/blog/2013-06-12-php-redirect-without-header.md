---
id: 705
title: 'PHP redirect without header()'
date: '2013-06-12T19:19:54+00:00'
author: kalpesh
layout: post
tags:
    - PHP
tags:
    - php
    - redirect
---

It’s very frustrating when you want to redirect from one page to another, and you get the error:

*Warning: Cannot modify header information – headers already sent by (output started at /some/filename.php:12) in /some/filename.php on line 99*

The problem is Headers are already sent, or in simple language the output is already sent to browser when your header() function is called. The best solution is not to pass headers (send html/output to browser) till the point header() function is fired.

Another way is to use output buffering. Without output buffering (the default), your HTML is sent to the browser in pieces as PHP processes through your script. With output buffering, your HTML is stored in a variable and sent to the browser as one piece at the end of your script. For using this method, you have to start your file with *ob_start();* so that output gets buffered.

But what if you don’t care whether the output is sent or not, you anyway want the redirect to work? This simple function will do the trick for you. It will check if headers are not sent, then it will call the PHP’s header function to redirect. But if the headers are sent, it will use Javascript to redirect to the URL you want.

{{< highlight php "style=emacs" >}}function redirect($url)  
{  
 if (!headers_sent())  
 {  
 header(‘Location: ‘.$url);  
 exit;  
 }  
 else  
 {  
 echo ‘<script type="text/javascript">';
        echo 'window.location.href="'.$url.'";';
        echo '</script>‘;  
 echo ‘<noscript>‘;  
 echo ‘<meta content="0;url='.$url.'" http-equiv="refresh"></meta>‘;  
 echo ‘</noscript>‘;  
 exit;  
 }  
}{{< /highlight >}}