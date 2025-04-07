---
id: 810
title: 'Magento get current url with and without parameters'
date: '2013-07-21T23:09:53+00:00'
author: kalpesh
layout: post
tags:
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