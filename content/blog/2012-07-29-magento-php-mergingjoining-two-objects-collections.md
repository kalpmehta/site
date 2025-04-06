---
id: 311
title: 'Magento, PHP: Merging/Joining two objects collections'
date: '2012-07-29T21:10:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=311'
permalink: /index.php/2012/07/29/magento-php-mergingjoining-two-objects-collections/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/26/php-xml-to-json-xml-to-array-json-to-array/"     class="crp_title">Convert PHP XML to JSON, XML to Array, JSON to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/"     class="crp_title">Magento join EAV collection with Flat table</a></li></ul></div>'
categories:
    - Magento
    - PHP
tags:
    - 'covert object collection to array'
    - 'magento array to collection'
    - 'magento array to object'
    - 'magento collection to array'
    - 'magento object to array'
    - 'php merging two objects'
---

It’s easy to merge two arrays with array_merge, but have you came across to merge two objects? It’s not that easy in Magento. You need to convert it to array first, merge them, and convert it to the object again to make it work. If you have two objects of different class, then it’s really difficult job to merge as both will not be compatible. If they are from similar classes or share same elements inside, then it’s not that tricky.

If you want to add collection2 in collection1 (in Magento), where collection1 will be a merged form of both, you can do so by:  
{{< highlight php "style=emacs" >}}foreach($collection2 as $coll) {  
 $collection1->addItem($coll);  
}{{< /highlight >}}  
  
In core PHP, it’s quite easy in this way:  
{{< highlight php "style=emacs" >}}$merged_obj = (object) array_merge( (array) $collection1, (array) $collection2 );{{< /highlight >}}

In Magento, converting collection to array is easy:  
{{< highlight php "style=emacs" >}}$arr = $collection->toArray();{{< /highlight >}}  
while vice versa is difficult as Magento doesn’t have any built-in method to do so.