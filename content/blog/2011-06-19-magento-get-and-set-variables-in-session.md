---
id: 93
title: 'Magento: Get and set variables in session'
date: '2011-06-19T07:56:21+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=93'
permalink: /index.php/2011/06/19/magento-get-and-set-variables-in-session/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-submitting-form-in-admin-redirects-to-dashboard/"     class="crp_title">Magento: Submitting form in admin redirects to dashboard</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li></ul></div>'
categories:
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