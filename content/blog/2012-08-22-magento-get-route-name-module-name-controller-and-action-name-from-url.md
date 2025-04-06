---
id: 322
title: 'Magento: Get route name, module name, controller and action name from URL'
date: '2012-08-22T15:03:52+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=322'
permalink: /index.php/2012/08/22/magento-get-route-name-module-name-controller-and-action-name-from-url/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li></ul></div>'
categories:
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