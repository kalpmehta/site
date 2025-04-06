---
id: 353
title: 'PHP: is_int() vs is_numeric()'
date: '2012-10-17T14:53:07+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=353'
permalink: /index.php/2012/10/17/php-is_int-vs-is_numeric/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/04/18/magento-get-sentence-case-from-camel-case-string/"     class="crp_title">Magento: Get sentence case from camel case string</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-and-set-variables-in-session/"     class="crp_title">Magento: Get and set variables in session</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li></ul></div>'
categories:
    - PHP
tags:
    - 'php check variable integer'
    - 'php is_int vs is_numeric'
---

Both of the functions looks similar, but there is a difference, which can screw your time if you’re not aware of it and using blindly! is_int() seems same to is_numeric(), checking the variable if it’s integer or not, but it’s not exactly what you’re thinking.

The key difference between these two functions is that is_int() checks the **type** of variable, while is_numeric() checks the **value** of the variable.

From PHP.net,  
*is_int:* Find whether the type of a variable is integer  
*is_numeric:* Finds whether a variable is a number or a numeric string

So, if you check something like:  
{{< highlight php "style=emacs" >}}$var = “123”;{{< /highlight >}}  
$var is a string of numbers, not an integer value.  
Therefor *is_int should return false* as it’s not an integer, it’s a string.  
However it is a numeric string, so hence *is_numeric should return true*.