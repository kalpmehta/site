---
id: 633
title: 'Magento clone collection &#8211; How to clone collection in Magento'
date: '2013-05-23T09:03:43+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=633'
permalink: /index.php/2013/05/23/magento-clone-collection-how-to-clone-collection-in-magento/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li><li><a href="http://ka.lpe.sh/2012/01/05/magento-wrong-count-in-admin-grid-when-using-group-by-clause-overriding-lib-module/"     class="crp_title">Magento: Wrong count in admin Grid when using GROUP BY clause, overriding lib module</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-mysql-records-null-values-not-getting-fetched/"     class="crp_title">Magento: Mysql records with NULL values are not fetched in query</a></li></ul></div>'
categories:
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