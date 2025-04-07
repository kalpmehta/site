---
id: 202
title: 'Magento/PHP: Convert your XML Object to Array'
date: '2012-02-12T06:24:25+00:00'
author: kalpesh
layout: post
tags:
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