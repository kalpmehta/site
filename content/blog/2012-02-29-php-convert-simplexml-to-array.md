---
id: 219
title: 'PHP Convert SimpleXML object to Array'
date: '2012-02-29T12:34:47+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=219'
permalink: /index.php/2012/02/29/php-convert-simplexml-to-array/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-category-object-from-category-name/"     class="crp_title">Magento: Get category object from category name</a></li><li><a href="http://ka.lpe.sh/2012/04/18/magento-get-sentence-case-from-camel-case-string/"     class="crp_title">Magento: Get sentence case from camel case string</a></li><li><a href="http://ka.lpe.sh/2012/07/26/php-xml-to-json-xml-to-array-json-to-array/"     class="crp_title">Convert PHP XML to JSON, XML to Array, JSON to Array</a></li><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li></ul></div>'
categories:
    - PHP
    - XML
tags:
    - convert
    - 'object to array'
    - 'simplexml to array'
---

In PHP, if you want to convert your xml data to array for looping and displaying purpose, it sometimes becomes tedious. If you already have a SimpleXML class and want to convert XML to Array without any notices, warnings and recursively preparing the array, here is the method that will do so without any modifications needed. This will work by pasting this in your class file, if you are not using object oriented approach, you will have to remove “public” and “$this->” from this function.

{{< highlight php "style=emacs" >}}public function simpleXMLToArray(SimpleXMLElement $xml,$attributesKey=null,$childrenKey=null,$valueKey=null){

 if($childrenKey &amp;&amp; !is_string($childrenKey)){$childrenKey = ‘@children’;}  
 if($attributesKey &amp;&amp; !is_string($attributesKey)){$attributesKey = ‘@attributes’;}  
 if($valueKey &amp;&amp; !is_string($valueKey)){$valueKey = ‘@values’;}

 $return = array();  
 $name = $xml->getName();  
 $_value = trim((string)$xml);  
 if(!strlen($_value)){$_value = null;};

 if($_value!==null){  
 if($valueKey){$return[$valueKey] = $_value;}  
 else{$return = $_value;}  
 }

 $children = array();  
 $first = true;  
 foreach($xml->children() as $elementName => $child){  
 $value = $this->simpleXMLToArray($child,$attributesKey, $childrenKey,$valueKey);  
 if(isset($children[$elementName])){  
 if(is_array($children[$elementName])){  
 if($first){  
 $temp = $children[$elementName];  
 unset($children[$elementName]);  
 $children[$elementName][] = $temp;  
 $first=false;  
 }  
 $children[$elementName][] = $value;  
 }else{  
 $children[$elementName] = array($children[$elementName],$value);  
 }  
 }  
 else{  
 $children[$elementName] = $value;  
 }  
 }  
 if($children){  
 if($childrenKey){$return[$childrenKey] = $children;}  
 else{$return = array_merge($return,$children);}  
 }

 $attributes = array();  
 foreach($xml->attributes() as $name=>$value){  
 $attributes[$name] = trim($value);  
 }  
 if($attributes){  
 if($attributesKey){$return[$attributesKey] = $attributes;}  
 else{$return = array_merge($return, $attributes);}  
 }

 return $return;  
}  
{{< /highlight >}}

Hope this helps.