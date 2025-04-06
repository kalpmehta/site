---
id: 810
title: 'Magento get current url with and without parameters'
date: '2013-07-21T23:09:53+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=810'
permalink: /index.php/2013/07/21/magento-get-current-url/
snapEdIT:
    - '1'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5764853657476534272&amp;type=U&amp;a=ZhQw";s:5:"pDate";s:19:"2013-07-21 23:10:17";}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"359087969606443009";s:5:"pDate";s:19:"2013-07-21 23:10:18";}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/08/22/magento-get-route-name-module-name-controller-and-action-name-from-url/"     class="crp_title">Magento: Get route name, module name, controller and action name from URL</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2013/06/12/php-redirect-without-header/"     class="crp_title">PHP redirect without header()</a></li></ul></div>'
snapFB:
    - 's:302:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200418398406795";s:5:"pDate";s:19:"2013-07-21 23:10:17";}}";'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - 'current url'
    - magento
---

You can get the current page URL and it’s parameters (if any) by using getCurrentUrl() method in Magento. Below code will show you how to use it. Consider for example you have this url:

http://loca.lho.st/review/product/list/id/27/name/sony

To get this (current) URL in your module:  
{{< highlight php "style=emacs" >}}$currentUrl = $this->helper(‘core/url’)->getCurrentUrl();  
//Gives: http://loca.lho.st/review/product/list/id/27/name/sony{{< /highlight >}}

To get current URL parameters:  
{{< highlight php "style=emacs" >}}$params = $this->getRequest()->getParams(); //all the parameters  
//Gives: Array ( [id] => 27 [name] => sony )  
$param = $this->getRequest()->getParam(‘name’); //parameter “name”  
//Gives: sony{{< /highlight >}}

To get only URL without parameters:  
{{< highlight php "style=emacs" >}}$request = $this->getRequest();  
$urlWithoutParameters = $this->getBaseUrl() . $request->getRouteName() .DS. $request->getControllerName() .DS. $request->getActionName();  
//Gives: http://loca.lho.st/review/product/list{{< /highlight >}}