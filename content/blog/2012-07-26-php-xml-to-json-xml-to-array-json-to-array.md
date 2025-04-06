---
id: 307
title: 'Convert PHP XML to JSON, XML to Array, JSON to Array'
date: '2012-07-26T19:02:00+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=307'
permalink: /index.php/2012/07/26/php-xml-to-json-xml-to-array-json-to-array/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2012/07/29/magento-php-mergingjoining-two-objects-collections/"     class="crp_title">Magento, PHP: Merging/Joining two objects collections</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li></ul></div>'
categories:
    - JSON
    - PHP
    - XML
tags:
    - array
    - json
    - 'php json to array'
    - 'php xml to array'
    - 'php xml to json'
    - xml
---

Converting PHP XML to JSON, XML to Array, JSON to Array is very difficult task for some people. But, in PHP, believe me it’s very easy. One line of code each! Don’t believe? Just check out the code below and test it yourself!  
{{< highlight php "style=emacs" >}}$xml = simplexml_load_string($xmlstring);  
$json = json_encode($xml);  
$arr = json_decode($json,true);{{< /highlight >}}  
Happy Coding!