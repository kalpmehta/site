---
id: 682
title: 'jQuery Prototype conflict, resolve it using noconflict'
date: '2013-06-01T20:37:42+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=682'
permalink: /index.php/2013/06/01/jquery-prototype-conflict/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/29/jquery-check-if-checkbox-is-checked/"     class="crp_title">jQuery check if checkbox is checked or not</a></li><li><a href="http://ka.lpe.sh/2013/05/29/jquery-redirect-page-with-javascript-alternative/"     class="crp_title">jQuery redirect page, with javascript alternative</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-get-email-address-and-created-updated-expires-dates-of-domain-name/"     class="crp_title">Linux: Bash script to get email address and created/updated/expires dates of domain name</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li></ul></div>'
categories:
    - jQuery
    - 'Prototype JS'
tags:
    - jquery
    - 'prototype js'
---

It’s difficult to use different javascript libraries in the same page. Because they tend to create conflicts with each other’s code, and often break javascript. One such case is using jQuery and PrototypeJS libraries in the same webpage. Both prototypejs and jquery use $ as their function or variable name which causes issues, as both the libraries will get triggered with that alias.

jQuery provides a method which solves this issue, so that you can use any javascript library with jQuery on the same page. This function is called [noConflict()](http://api.jquery.com/jQuery.noConflict/), and it simply uses different symbol/charater(s) you provide rather than dollar ($).

Below code will help you to understand this and you can use it to resolve conflicts between different javascript libraries used when using jQuery on the same page.

{{< highlight js "style=emacs" >}}<script src="prototype.js" type="text/javascript"></script>  
<script src="jquery.js" type="text/javascript"></script>  
<script type="text/javascript">
    var $j = jQuery.noConflict();
</script>{{< /highlight >}}

After using the above code, you can use jQuery as $j and PrototypeJS as $.