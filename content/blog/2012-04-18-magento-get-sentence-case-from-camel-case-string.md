---
id: 252
title: 'Magento: Get sentence case from camel case string'
date: '2012-04-18T17:31:06+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=252'
permalink: /index.php/2012/04/18/magento-get-sentence-case-from-camel-case-string/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2012/10/17/php-is_int-vs-is_numeric/"     class="crp_title">PHP: is_int() vs is_numeric()</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2012/07/29/magento-php-mergingjoining-two-objects-collections/"     class="crp_title">Magento, PHP: Merging/Joining two objects collections</a></li></ul></div>'
categories:
    - Magento
    - PHP
tags:
    - 'camel case to sentence case'
    - 'camelize to underscore'
    - 'magento getter setter'
---

Magento has pre-defined methods for getters and setters which will convert camelcase string to underscore formatted string.  
Example, Magento will convert *thisIsDummy* to *this_is_dummy* using it’s method _underscore which is available at Varien_Object class.

If you want to convert **Camel case string to Sentence case** (this may sound weird, but we got the requirement),  
Example, from *thisIsDummy* to *This Is Dummy*, below method will help you to do so:

{{< highlight php "style=emacs" >}}public function camelToSentence($word) {  
 if(isset($word)) {  
 $result = ucwords(preg_replace(‘/(.)([A-Z])/’, “$1 $2”, $word));  
 return $result;  
 }  
 }{{< /highlight >}}