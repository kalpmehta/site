---
id: 252
title: 'Magento: Get sentence case from camel case string'
date: '2012-04-18T17:31:06+00:00'
author: kalpesh
layout: post
tags:
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