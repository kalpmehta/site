---
id: 322
title: 'Magento: Get route name, module name, controller and action name from URL'
date: '2012-08-22T15:03:52+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'get controller action name'
    - 'get module name'
    - 'get route name'
    - magento
---

Getting route name, module name, controller name and action name is very easy in Magento. You can get these values anywhere, in controller itself and also in template files.

{{< highlight php "style=emacs" >}}Mage::app()->getRequest()->getControllerName();

Mage::app()->getRequest()->getActionName();

Mage::app()->getRequest()->getRouteName();

Mage::app()->getRequest()->getModuleName();{{< /highlight >}}