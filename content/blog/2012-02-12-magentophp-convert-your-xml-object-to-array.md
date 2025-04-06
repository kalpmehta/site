---
id: 202
title: 'Magento/PHP: Convert your XML Object to Array'
date: '2012-02-12T06:24:25+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=202'
permalink: /index.php/2012/02/12/magentophp-convert-your-xml-object-to-array/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2012/07/26/php-xml-to-json-xml-to-array-json-to-array/"     class="crp_title">Convert PHP XML to JSON, XML to Array, JSON to Array</a></li><li><a href="http://ka.lpe.sh/2012/07/29/magento-php-mergingjoining-two-objects-collections/"     class="crp_title">Magento, PHP: Merging/Joining two objects collections</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2012/04/18/magento-get-sentence-case-from-camel-case-string/"     class="crp_title">Magento: Get sentence case from camel case string</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - PHP
tags:
    - 'convert xml to array'
    - magento
    - simplexml
    - 'simplexml to array'
---

While developing shipment tracking using SimpleXML in magento, I came accross the requirement where I have to get all the XML tags as keys and all the data inside XML tags as values in array. Means I wanted to convert XML to an Array where I can display all the information in some decorative format.

So here is how I converted XML to Array without any kind of hardcoding.

**PHP class method to convert xml to array**  
{{< highlight php "style=emacs" >}}  
public function convertXmlObjToArr($obj, &amp;$arr){  
 $children = $obj->children();  
 $executed = false;  
 foreach ($children as $elementName => $node){  
 if($arr[$elementName]!=null){  
 if($arr[$elementName][0]!==null){  
 $i = count($arr[$elementName]);  
 $this->convertXmlObjToArr($node, $arr[$elementName][$i]);  
 }else{  
 $tmp = $arr[$elementName];  
 $arr[$elementName] = array();  
 $arr[$elementName][0] = $tmp;  
 $i = count($arr[$elementName]);  
 $this->convertXmlObjToArr($node, $arr[$elementName][$i]);  
 }  
 }else{  
 $arr[$elementName] = array();  
 $this->convertXmlObjToArr($node, $arr[$elementName]);  
 }  
 $executed = true;  
 }  
 if(!$executed&amp;&amp;$children->getName()==””){  
 $arr = (String)$obj;  
 }  
 return;  
 }

{{< /highlight >}}  
Hope this helps!