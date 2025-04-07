---
id: 276
title: 'Magento Interview questions and answers'
date: '2012-07-19T11:25:13+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento Interview'
tags:
    - answers
    - interview
    - magento
    - 'magento interview questions'
    - questions
---

Magento Interview questions and answers for freshers as well as experienced developers.

**1. Explain Magento’s MVC architecture**

*First of all, what is MVC?*

MVC stands for **Model-View-Controller**. Any application that separates it’s data access, business logic and user interface is called MVC. There can be two types of MVC: **convention-based and configuration-based**. Example, cakePHP is convention-based, i.e. you just need to follow the instructions of the core system to get your module ready in just few lines. Magento is configuration-based, i.e. you need to specify each and every thing to your module’s config file in order to get it work. Magento has controllers (for request/response routing), Block (for rendering content), Model (for business logic), Resource/Mysql4 (for database operations), etc (for module-specific configuration files), Helper (for common functions), sql (for setup scripts), layout (for connecting block with templates for each controller action) and template/.PHTML file (for Presentation i.e. View).  
  
*How Magento’s MVC works:*

1\. When you enter the URL (something like http://loca.lho.st/frontname/controller/method/param1/value1/param2/value2), this URL is intercepted by one PHP file called index.php which instantiates Magento application  
2\. Magento application instantiates Front Controller object  
3\. Further, front controller instantiates Router objects (specified in module’s config.xml, global tag)  
4\. Now, Router is responsible to “match” the frontname which is in our URL  
5\. If “match” is found, it sees controller name and method name in the URL, which is finally called.  
6\. Now depending on what is written in action name (method name), it is executed. If any models are called in it, the controller method will instantiate that model and call the method in it which is requested.  
7\. Then the controller action (method) instantiate the Layout object, which calls Block specified for this action (method) name (Each controller action name have block and template file associated with it, which can be found at app/design/frontend or adminhtml/namespace/module/layout/module.xml file, name of layout file (module.xml) can be found in config.xml of that module, in layout updates tag).  
8\. Template file (.phtml) now calls the corresponding block for any method request. So, if you write $this->methodName in .phtml file, it will check “methodName” in the block file which is associated in module.xml file.  
9\. Block contains PHP logic. It references Models for any data from DB.  
10\. If either Block, Template file or Controller need to get/set some data from/to database, they can call Model directly like Mage::getModel(‘modulename/modelname’).  
For diagramatic view: [click here](http://alanstorm.com/2009/img/magento-book/magento-mvc.png) (courtsey: Alan Storm)

**2. How Magento ORM works?**

ORM stands for **Object Relational Mapping**. It’s a programming technique used to convert different types of data to Objects and vice versa.

In Magento, ORM is shown as Model (based on Zend Framework’s Zend_Db_Adapter), which further breaks down to two types of Models.

– First is the “simple” i.e. **Regular** Models which is nothing but flat table or our regular table structure.  
– Second Model is **EAV** (Entity Attribute Value), which is quite complicated and expensive to query.

All Magento Models interacting with database are inherited from Mage_Core_Model_Abstract class, which is further inherited from Varien_Object.

Difference between two Models is, Simple Model is inherited from *Mage_Core_Model_Resource_Db_Abstract* class,  
while EAV is inherited from *Mage_Eav_Model_Entity_Abstract*.

For those who don’t know what EAV is, please read my 3rd answer below.

So, to end up this question,  
when you want to get some data in Magento, you call it like this:  
{{< highlight php "style=emacs" >}}Mage::getModel(‘module/model’)->load(1);{{< /highlight >}}  
where 1 is the primary key id for some Regular/Simple table, while in EAV so many tables are joined to fetch just single row of data.

**3. What is EAV in Magento?**

EAV, stands for **Entity Attribute Value**, is a technique which allows you to add unlimited columns to your table virtually. Means, the fields which is represented in “column” way in a regular table, is represented in a “row” (records) way in EAV. In EAV, you have one table which holds all the “attribute” (table field names) data, and other tables which hold the “entity” (id or primary id) and value (value for that id) against each attribute.

In Magento, there is one table to hold attribute values called *eav_attribute* and 5-6 tables which holds entity and data in fully normalized form,

– eav_entity, eav_entity_int (for holding Integer values),  
– eav_entity_varchar (for holding Varchar values),  
– eav_entity_datetime (for holding Datetime values),  
– eav_entity_decimal (for holding Decimal/float values),  
– eav_entity_text (for holding text (mysql Text type) values).

EAV is expensive and should only be used when you are not sure about number of fields in a table which can vary in future. To just get one single record, Magento joins 4-5 tables to get data in EAV. But this doesn’t mean that EAV only has drawbacks. The main **advantage of EAV** is when you may want to add table field in future, when there are thousands or millions of records already present in your table. In regular table, if you add table field with these amount of data, it will screw up your table, as for each empty row also some bytes will be allocated as per data type you select. While in EAV, adding the table column will not affect the previously saved records (also the extra space will not get allocated!) and all the new records will seamlessly have data in these columns without any problem.

**4. Difference between Mage::getSingleton() and Mage::getModel()**

The difference between Mage:getSingleton() and Mage::getModel() is that the former one does not create an object if the object for same class is already created, while the later creates new objects every time for the class when it’s called.

Mage::getSingleton() uses the “**singleton design pattern**” of PHP. If the object is not created, it will create it.

Mage::getSingleton() is mostly used when you want to create an object once, modify it and later fetch from it. Popular example is session, you first create a session object, and then add/remove values from session across different pages, so that it retains your values (e.g. cart values, logged in customer details, etc.) and doesn’t create new session object losing your last changes.

Mage::getModel() is used when you want to have the fresh data from the database. Example is when you want to show records from database.

**8. How will you call a CMS page in your module’s PHTML file?**

$this->getLayout()->createBlock(‘cms/block’)->setBlockId(‘blockidentifier’)->toHtml();

**9. What is codePool in Magento?**

codePool is a tag which you have to specify when registering new module in app/etc/modules/Company_Module.xml  
There are 3 codePools in Magento: core, community and local, which are resided at app/code/ directory.  
Core codePool is used by Magento core team, Community is generally used by 3rd party extensions and Local codePool should be used for in-hour module development and overriding of core and community modules for custom requirement.  
So in short, codePool helps Magento to locate module inside app/code/ for processing.

**15. When will you need to clear cache to see the changes in Magento?**

When you have added/modified XML, JS, CSS file(s).

**17. How will you enable product’s custom attribute visibility in frontend?**

In the *Manage Attributes* section of the custom attribute, select *Visible on Product View Page on Front-end* and *Used in Product Listing* to *Yes*.

**19. Difference between EAV and flat model**

EAV is entity attribute value database model, where data is fully in normalized form. Each column data value is stored in their respective data type table. Example, for a product, product ID is stored in catalog_product_entity_int table, product name in catalog_product_entity_varchar, product price in catalog_product_entity_decimal, product created date in catalog_product_entity_datetime and product description in catalog_product_entity_text table. EAV is complex as it joins 5-6 tables even if you want to get just one product’s details. Columns are called attributes in EAV.

Flat model uses just one table, so it’s not normalized and uses more database space. It clears the EAV overhead, but not good for dynamic requirements where you may have to add more columns in database table in future. It’s good when comes to performance, as it will only require one query to load whole product instead of joining 5-6 tables to get just one product’s details. Columns are called fields in flat model.

**20. Is it mandatory to give Namespace while creating custom module in Magento?**

No

**21. How will you override Block/Model/controllers in Magento?**

[http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/](http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/ "Magento override block controller model helper")

**23. How will you add/remove content from core’s system.xml file?**

You can do that by overriding system.xml configuration. Examples:  
{{< highlight xml "style=emacs" >}}<config>  
 <sections> <catalog>  
 <groups>  
 <frontend>  
 <label>Overriding Catalog Frontend in system config</label>  
 </frontend>  
 </groups>  
 </catalog>  
 </sections></config>{{< /highlight >}}  
{{< highlight xml "style=emacs" >}}<config>  
 <sections> <payment> <groups>  
 <cashondelivery>  
 <fields>  
   
 </fields>  
 </cashondelivery>  
 </groups> </payment> </sections></config>{{< /highlight >}}

**24. Can you have more than one Grid in a module?**

Yes

**25. How will you join flat table and EAV table in Magento?**

[http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/](http://ka.lpe.sh/2013/04/28/magento-join-eav-collection-with-flat-table/ "Magento Join EAV collection with flat table")

**26. How will you enable maintenance mode of your Magento website?**

[http://ka.lpe.sh/2011/12/31/magento-show-maintenance-mode-page-website-under-construction/](http://ka.lpe.sh/2011/12/31/magento-show-maintenance-mode-page-website-under-construction/ "Magento show maintenance mode")

**27. What are “magic methods” in Magento?**

Magento uses __call(), __get(), __set(), __uns(), __has(), __isset(), __toString(), __construct(), etc. magic methods. You can find more details inside class Varien_Object  
For more information about magic methods: [http://php.net/manual/en/language.oop5.magic.php](http://php.net/manual/en/language.oop5.magic.php "PHP magic methods")

**28. How many database tables will Magento create when you make a new EAV module?**

Magento creates 6 tables when you create new EAV module. Tables: module, module_datetime, module_decimal, module_int, module_text and module_varchar. one is the main entity table, and rest 5 tables which holds attribute’s data in different data types. So that integer values will go to module_int table, price values to module_decimal, etc.

**33. Where will you write your module’s business logic in Magento?**

inside Model

**34. Explain different types of sessions in Magento (e.g. customer/session, checkout/session, core/session) and the reason why you store data in different session types?**

Customer sessions stores data related to customer, checkout session stores data related to quote and order. They are actuall under one session in an array. So firstname in customer/session will be $_SESSION[‘customer’][‘firstname’] and cart items count in checkout/session will be $_SESSION[‘checkout’][‘items_count’]. The reason Magento uses session types separately is because once the order gets placed, the checkout session data information should get flushed which can be easily done by just unsetting $_SESSION[‘checkout’] session variable. So that the session is not cleared, just session data containing checkout information is cleared and rest all the session types are still intact.

**35. What are the commonly used block types? What is the special in core/text_list block type.**

Commonly used block types: core/template, page/html, page/html_head, page/html_header, page/template_links, core/text_list, page/html_wrapper, page/html_breadcrumbs, page/html_footer, core/messages, page/switch.  
Some blocks like content, left, right etc. are of type core/text_list. When these blocks are rendered, all their child blocks are rendered automatically without the need to call getChildHtml() method.

**36. What are the different design patterns used in Magento?**

[http://ka.lpe.sh/2013/02/25/magento-design-patterns/](http://ka.lpe.sh/2013/02/25/magento-design-patterns/ "Magento design patterns")

**37. What can you do to optimize Magento performance?**

[http://ka.lpe.sh/category/performance/](http://ka.lpe.sh/category/performance/ "Magento Performance")

**38. Where is the relation between configurable product and it’s simple product stored in database?**

In the 2 tables:  
catalog_product_relation  
catalog_product_superlink_table

**39. How will you log current collection’s SQL query?**

$collection->printLogQuery(true); OR $collection->getSelect()->__toString();

**40. How to get first item or last item from the collection?**

$collection->getFirstItem() and $collection->getLastItem();

For more Magento interview questions for freshers and experienced developers, check this:  
[Magento Interview Questions for Experienced and Freshers](http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/ "Magento Interview Questions for Experienced and Freshers")