---
id: 32
title: 'Magento 1.5: Cannot login to admin panel after fresh install'
date: '2011-06-05T07:11:19+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=32'
permalink: /index.php/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/12/magento-get-rid-of-admin-notifications-pop-up/"     class="crp_title">Magento: Get rid of admin notifications pop-up</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-submitting-form-in-admin-redirects-to-dashboard/"     class="crp_title">Magento: Submitting form in admin redirects to dashboard</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2012/01/05/magento-wrong-count-in-admin-grid-when-using-group-by-clause-overriding-lib-module/"     class="crp_title">Magento: Wrong count in admin Grid when using GROUP BY clause, overriding lib module</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
tags:
    - error
    - magento
---

After installing magento 1.5, I tried to login to the admin panel with correct username and password, but it does not let me in without any error message. This is due to cookie problem in magento and can be fixed as below:

Open this file in your favorite editor: **app/code/core/Mage/Core/Model/Session/Abstract/Varien.php**

Comment lines that says like (probably line number 81 to 83)  
{{< highlight php "style=emacs" >}}  
$this->getCookie()->getDomain(),  
$this->getCookie()->isSecure(),  
$this->getCookie()->getHttponly()  
{{< /highlight >}}  
to  
{{< highlight php "style=emacs" >}}  
//$this->getCookie()->getDomain(),  
//$this->getCookie()->isSecure(),  
//$this->getCookie()->getHttponly()  
{{< /highlight >}}  
Now you could login to your admin panel without any problem.