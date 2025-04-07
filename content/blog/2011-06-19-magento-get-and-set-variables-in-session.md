---
id: 93
title: 'Magento: Get and set variables in session'
date: '2011-06-19T07:56:21+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - magento
    - session
---

Suppose you want to set data in the magento session, so that you can retrieve it from other pages. Session has been very useful global variable in PHP and using it we can easily retrieve and add data to it and get it from the entire site.

Here is the code that will set / add your custom data into session.  
{{< highlight php "style=emacs" >}}Mage::getSingleton(‘core/session’)->setMyCustomData(‘blah’);{{< /highlight >}}

here, setMyCustomData can be replaced with the meaningful name as per your need. One thing to be cautious while setting session variables is to make sure it doesn’t conflict with magento’s internal variables, example setData.

Code to retrieve the session variable  
{{< highlight php "style=emacs" >}}$session = Mage::getSingleton(‘core/session’, array(‘name’ => ‘frontend’));  
echo $session->getMyCustomData();{{< /highlight >}}