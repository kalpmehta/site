---
id: 633
title: 'Magento clone collection &#8211; How to clone collection in Magento'
date: '2013-05-23T09:03:43+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - clone
    - collection
    - magento
---

Clone collection in Magento in an easy and effective way. Cloning collection in Magento is not as straight forward as we do in PHP object cloning. That’s because Magento does not implement clone in it’s collection object, which is why if you try to clone Magento collection it will nothing but just a copy of the original collection itself. If the original collection gets updated, this cloned will also get updated, which is what we don’t want right?

Let’s see an example where PHP’s clone keyword will fail. Consider you have an $collection in the class method and you want to perform operations on this $collection in two different ways. So you need to clone this $collection and perform operation differently in both the collections so that both collections have different result set.

{{< highlight php "style=emacs" >}}$coll1 = clone $collection;  
$coll2 = clone $collection;{{< /highlight >}}

Let’s perform different operations on these two separate collections now, like this:

{{< highlight php "style=emacs" >}}$coll1->getSelect()->where(‘first where condition’);  
$coll2->getSelect()->where(‘second where condition’);  
if($coll1->getSize() == 0) {  
 $collection = $coll2;  
} else {  
 $collection = $coll1;  
}{{< /highlight >}}

But this will fail and not work what we expect here. $collection here will hold BOTH the where conditions, instead of any one depending on the result of IF condition.

To overcome this, in Magento, what you have to do is:  
  
{{< highlight php "style=emacs" >}}//Assuming you have original collection as $collection  
$collection->getSelect()  
 ->joinLeft(‘table1 as table1alias’, ‘table1alias.entity_id=e.entity_id’,array(‘name’,’description’))  
 ->where(‘$firstWhereCondition’);

$coll = clone $collection;  
if($coll->getSize() == 0) {  
 $fromPart = $collection->getSelect()->getPart(Zend_Db_Select::FROM); //getting all the FROM clause from collection  
 $wherePart = $collection->getSelect()->getPart(Zend_Db_Select::WHERE); //getting all the WHERE clause conditions from collection  
 //debug to see what you have to remove  
 //print_r($fromPart);print_r($wherePart);exit;

 unset($fromPart[‘table1alias’]); //removing table1 join which we did for first where condition  
 unset($wherePart[0]); //removing first where condition, this may be different based on your query

 //removed FROM and first WHERE condition from collection  
 $collection->getSelect()->setPart(Zend_Db_Select::FROM, $fromPart);  
 $collection->getSelect()->setPart(Zend_Db_Select::WHERE, $wherePart);

 //now assign FROM and second WHERE condition to collection  
 $collection->getSelect()  
 ->joinLeft(‘table1 as table1alias’, ‘table1alias.entity_id=e.entity_id’,array(‘name’,’description’))  
 ->where($secondWhereCondition);

 //echo $collection->getSelect()->__toString();

}  
echo $collection->getSize();{{< /highlight >}}

That’s it! You have just used one collection and applied two where conditions. Similarly you can even apply multiple FROM and WHERE clause conditions as per the requirement.

HTH!