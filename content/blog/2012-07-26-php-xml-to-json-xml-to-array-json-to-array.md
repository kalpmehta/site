---
id: 307
title: 'Convert PHP XML to JSON, XML to Array, JSON to Array'
date: '2012-07-26T19:02:00+00:00'
author: kalpesh
layout: post
tags:
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