---
id: 491
title: 'Magento: Design Patterns'
date: '2013-02-25T11:06:20+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=491'
permalink: /index.php/2013/02/25/magento-design-patterns/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li></ul></div>'
categories:
    - Magento
tags:
    - decorator
    - 'event observer'
    - factory
    - helper
    - iterator
    - 'lazy loading'
    - 'magento design patterns'
    - prototype
    - registry
    - singleton
---

**Factory:**

It implement the concept of factories and deals with the problem of creating objects without specifying the exact class of object that will be created.  
{{< highlight php "style=emacs" >}}$product = Mage::getModel(‘catalog/product’);{{< /highlight >}}

**Singleton:**

It restricts the instantiation of a class to one object. It will refer to same object each time called.  
{{< highlight php "style=emacs" >}}$category = Mage::getSingleton(‘catalog/session’);{{< /highlight >}}

**Registry:**

It is a way to store information throughout your application.  
{{< highlight php "style=emacs" >}}Mage::register(‘key’,$value); //stores  
$currentCategory = Mage::registry(‘key’); //retrives{{< /highlight >}}

**Prototype:**

It determines the type of object to create. In Magento it can be Simple, Configurable, Grouped, Bundle, Downloadable or Virtual types.  
{{< highlight php "style=emacs" >}}Mage:getModel(‘catalog/product’)->getTypeInstance();{{< /highlight >}}

**Observer:**

It is mainly used to implement distributed event handling systems. Here the subject maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.  
{{< highlight php "style=emacs" >}}Mage::dispatchEvent(‘event_name’, array(‘key’=>$value));{{< /highlight >}}

{{< highlight xml "style=emacs" >}}<config>  
 <global>  
 <events>  
 <event_name>  
 <observers>  
 <unique_name>  
 <class>Class_Name</class>  
 <method>methodName</method>  
 </unique_name>  
 </observers>  
 </event_name>  
 </events>  
 </global>  
</config>{{< /highlight >}}  
  
**Object Pool:**

It is used to reuse and share objects that are expensive to create.  
{{< highlight php "style=emacs" >}}$id = Mage::objects()->save($object);  
$object = Mage::objects($id);{{< /highlight >}}

**Iterator:**

It is used to traverse a collection and access the collection’s items.  
{{< highlight php "style=emacs" >}}Mage::getModel(‘catalog/product’)->getCollection();{{< /highlight >}}

**Lazy Loading:**

It is used to defer initialization of an object until the point at which it is needed.  
{{< highlight php "style=emacs" >}}$collection_of_products = Mage::getModel(‘catalog/product’)  
->getCollection();{{< /highlight >}}

**Decorator:**

It is used to extend or modify the behaviour of an object at runtime.  
{{< highlight html "style=emacs" >}}<script type="text/javascript">decorateTable('product_comparison');</script>{{< /highlight >}}

**Helper:**

Multiple methods are available for use by other objects. Here you can use core’s helper methods from anywhere in the application.  
{{< highlight php "style=emacs" >}}Mage::helper(‘core’);{{< /highlight >}}

**Service Locator:**

Allows overrides or renamed physical resources (e.g. Classes, DB tables, etc)  
{{< highlight php "style=emacs" >}}Mage::getModel(‘catalog/product’) and $installer->getTable(‘customer/address_entity’);{{< /highlight >}}

Thanks to contributors at: <http://stackoverflow.com/questions/5041473/magento-design-patterns>