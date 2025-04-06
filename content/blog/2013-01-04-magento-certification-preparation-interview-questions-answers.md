---
id: 424
title: 'Magento Certification Preparation / Interview Questions Answers'
date: '2013-01-04T11:28:05+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=424'
permalink: /index.php/2013/01/04/magento-certification-preparation-interview-questions-answers/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li></ul></div>'
categories:
    - Magento
    - 'Magento Certification'
    - 'Magento Interview'
tags:
    - answers
    - certification
    - interview
    - magento
    - 'magento interview questions'
    - preparation
    - questions
    - 'study guide'
---

Hi guys, here is the stuff I collected and created from myriad number of websites/blogs/forums/ magento source codebase during my Magento certification preparation. I have put all the things I found and studied during my preparation in one place, so that other developers who are preparing for the exam can benefit from it.

Credits to all who have contributed these things over the web from where I copied for study purpose. Few credits to me as well as I also have contributed many things in it 🙂 This may contain errors and wrong information and I don’t guarantee it to be completely correct. But this should be a good resource if you want a heads up! Please be aware that you need to go through the study guide and fundamental videos yourself in order to pass this exam.

*If you are here to prepare for Interview, then I would recommend you to also go through these links:*  
[Magento Interview questions and answers](http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/ "Magento Interview questions and answers")  
[Magento Advanced Interview questions/](http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/ "Magento Advanced Interview questions")

The below stuff alone will definitely not going to help you much in passing the exam. Not to mention, these resource can also be used for Magento interview preparation.

  
{{< highlight html "style=emacs" >}}  
Magento supports and loads translations in the following order:

 – Module Translation CSV in /app/locale  
 – Theme Translation CSV in /app/design/

<area></area>/<package>/<theme>/locale (theme folder translate)  
 – DB Translation Database (table core_translate) ——-  
How many options exist to add a custom translation for any given string?

 As mentioned above, there are three options in Magento to add a custom translation to a text string: module translation, theme translation and inline translation.

 1. Module translation

 Module translations are stored in app/locale/languagecode_COUNTRYCODE/ folder in form of csv files, named as Namespace_Modulename.csv All string in extensions that are inside __() method can be translated this way

 2. Theme translation

 Strings can be translated inside your theme, for that you just need to set locale via Magento admin area, then create translate.csv in app/design/frontend/<package>/<theme>/locale/ languagecode_COUNTRYCODE and put your translated strings inside this CSV  
 “My Cart”,”My Basket”  
 “My Account”,”Account”</theme></package>

 3. Inline translation

 To enable inline translation you need to log into Admin panel and go to System -> Configuration -> Developer.  
 You need to select Store view from scope select and enable inline translation for this desired store view there.

——-

Magento uses the Front Controller pattern for the following purposes:

 Receiving and processing browser data, transferring it to other system elements;  
 Defining controller and proper action to perform using routes;  
 Displaying browser-requested data using blocks, templates and model data.

——-

(Front Controller) Routes processing order

 – admin

 – standard

 – cms

 – default  
——-

Mage::getModel() => getModelInstance() => getModelClassName() => new ClassNameInitializes…

 Mage :: getModel($modelClass, $arguments){  
 Mage_Core_Model_Config :: getModelInstance($modelClass, $arguments){  
 $className = $this->getModelClassName($modelClass){  
 return $this->getGroupedClassName(‘model’, $modelClass)  
 }  
 …  
 $obj = new $className($arguments);  
 }  
 }

——-  
Front Controller events… Mage_Core_Controller_Varien_Front

controller_front_init_before  
controller_front_init_routers  
controller_front_send_response_before  
controller_front_send_response_after

——-  
Mage_Core_Controller_Varien_Action fires events…

controller_action_layout_load_before  
controller_action_layout_generate_xml_before  
controller_action_layout_generate_blocks_before  
controller_action_layout_generate_blocks_after  
controller_action_layout_render_before  
controller_action_layout_render_before_{getFullActionName}  
controller_action_predispatch  
controller_action_predispatch_{getRouteName}  
controller_action_predispatch_{getFullActionName}  
controller_action_postdispatch  
controller_action_postdispatch_{getFullActionName}  
controller_action_postdispatch_{getRouteName}  
controller_action_noroute  
controller_action_nocookies

——-

http://blog.belvg.com/magento-front-controller-pattern.html  
http://magebase.com/magento-tutorials/digging-deeper-into-magentos-layout-xml-part-2/

——-  
The layout initialization happens as follows:

 1. Instances of the Layout and Layout Update are created.  
 2. Layout handles are added according to the $handles argument if passed.  
 3. Store layout handle STORE_[store_code] is added to the Layout Update Instance. For example, if code of current store is en, then layout handle STORE_en is added.  
 4. Theme layout handle THEME_[area]_[package]_[layout_theme] is added to the Layout Update Instance. For example, if the page rendered is for the frontend area, the current theme package name is magebase and theme name for layout is modern, then the layout handle THEME_frontend_magebase_modern is added.  
 5. Action layout handle is added to the Layout Update Instance. For example, if the page rendered is a category detail page, then Magento is executing catalog module’s category controller’s view action. So it will add an action handle catalog_category_view.  
 6. All Layout XML files defined for all active modules are loaded  
 7. If a layout file named local.xml exists in the current theme’s layout folder, it is loaded last  
 8. Layout updates of all added layout handles from the loaded layout XML are merged  
 9. Layout updates of all added layout handles from the database are merged  
 10. If the $generateXML argument of loadLayout() method is passed as false, the initialization is finished.  
 11. The layout update data is refined by removing all blocks and block references defined with the remove tag. (As discussed in Part 1)  
 12. If $generateBlocks argument is passed as false, the initialization is finished.  
 13. The instances of block classes are created according to the block definitions in the Layout XML  
 14. The methods are called with specified arguments on the blocks where action tags are defined. (As discussed in Part 1)  
——-

A layout should have at least one *output* block. Normally, the root block is the only output block in a layout but there can be multiple output blocks for a single page. In that case, the output of each output block is merged and returned in the response.

The *non-output* blocks are child blocks of output blocks and are normally rendered with the getChildHtml() method. There are also two other methods: getChildChildHtml() and getBlockHtml() also used to render non-output blocks.  
——-

Blocks can be instantiated via layout xml (<block addblock="" after="" and="" config="" createblock="" crontab="" file="" finally="" for="" getblock="" in="" initialization="" invokes="" located="" mage_core_model_layout="" mage_cron_model_observer-="" magento="" methods="" of="" section="" type="”groupName/setup”…),">dipatch() that does the following:</block>

Process scheduled cron queue: Magento reads the cron schedule table for jobs that need to be executed this very second and jobs that should have already been executed, i.e. with timestamps in the past, that haven’t expired. The expiry limit is also a parameter, configurable in the admin panel. After all the work, dispatch method calls two generate() and cleanup() methods

 Generate tasks schedule: Mage_Cron_Model_Observer->generate(), this method searches final configuration file for content of <crontab> nodes ($config = Mage::getConfig()->getNode(‘crontab/jobs’); ), reading <schedule><cron_expr> elements to find out when and how often they need to be executed and pulls this data into the cron_schedule table.</cron_expr></schedule></crontab>

 Cleanup: Mage_Cron_Model_Observer->cleanup(), this method deletes completed (with ‘success’ status) or missed ($time < $now – $scheduleLifetime, where $scheduleLifetime are set in Magento admin area) jobs from cron_schedule DB table. ------- 1. All .xml files are collected into one big simpleXmlElement object 2. First, data is loaded from app/etc/*.xml and then from app/etc/modules/*.xml. Based on the module loaded information, config.xml is loaded from the etc directory of the module. If we load backend to check ACL and build menu elements, adminhtml.xml and system.xml are loaded as well. Configuration data from the database is the last one to load. 3. Any parameters, except the ones stored in app/etc/local.xml, can be overridden in config.xml of a custom module. P.S. Even though Magento provides us with such convenient methods as Mage:: getStoreConfig() and Mage:: getStoreConfigFlag(), we can reach any element of the configuration tree with the help of Mage::getConfig()->getNode($path, $scope, $scopeCode);

——-  
Difference: A Website, a Store and a Store View.

 Each websites has its unique customer and order base, base currency and prices.  
 Stores can be used to define for example different (looking) stores with the same information.  
 Store Views are mostly used to handle different languages on your website. You will typically have one Store View per language.

———-  
Setting And Getting Cookies

 To set cookies:

 Mage::getModel(‘core/cookie’)->set(‘cookie_name’, ‘cookie_value’, 0); # session cookie  
 Mage::getModel(‘core/cookie’)->set(‘cookie_name’, ‘cookie_value’, 60); #lasts 60 seconds

 To get cookies:

 Mage::getModel(‘core/cookie’)->get(‘made_productalerts_stock’);

———-

Sending Transactional E-Mails

 $email = Mage::getModel(‘core/email_template’);

 $email->sendTransactional(  
 ‘some_email_template’, // template  
 array(‘name’ => ‘Your Company’, ’email’ => ‘contact@yourcompany.com’), // sender details  
 ‘joe@joebloggs.com’, // recipient email  
 ‘Joe Bloggs’, // recipient name  
 array(‘customerName’ => ‘Joe Bloggs’), // merge vars  
 Mage::app()->getStore()->getStoreId() // store id  
 );

———-  
Resizing A Product Image

 $helper = Mage::helper(‘catalog/image’);  
 $helper->init($product, ‘image’);  
 $helper->resize(216, 161);

———-  
Adding A Layout Handle From A Controller

 If you really need to add a handle to a controller, you need to replace the call to $this->loadLayout() with:

 $update = $this->getLayout()->getUpdate();  
 $update->addHandle(‘default’);  
 $this->addActionLayoutHandles();  
 $update->addHandle(‘your_handle’);  
 $this->loadLayoutUpdates();  
 $this->generateLayoutXml();  
 $this->generateLayoutBlocks();  
 $this->_isLayoutLoaded = true;

————

Config URL Rewrite Definition

 xpath: global/rewrite/module/from&amp;to  
 <config>  
 <global>  
 <rewrite>  
 <namespace_module>  
 <from><![CDATA[#^/some/regex/([a-z]*/?$#]]></from>  
 <to><![CDATA[/frontname/whatever/whatever/blah/$1]]></to>  
 </namespace_module>  
 </rewrite>  
 </global>  
 </config>  
———-  
Config Model Rewrite Definition

 xpath: global/models/catalog/rewrite/product  
 <config>  
 <global>  
 <models>  
 <catalog>  
 <rewrite> <product>Namespace_Module_Catalog_Product</product> </rewrite>  
 </catalog>  
 </models>  
 </global>  
 </config>

———-  
Overriding A Controller

 xpath: frontend/routers/checkout/args/modules/  
 <config>  
 <frontend>  
 <routers>  
 <checkout>  
 <args>  
 <modules>  
 <your_module before="Mage_Checkout">Your_Module_Checkout</your_module>  
 </modules>  
 </args>  
 </checkout>  
 </routers>  
 </frontend>  
 </config>

———-  
Config Transactional Email Template Definition

 <config>  
 <global>  
 <template>  
 <email>  
 <your_module_email_something_template module="namespace_module" translate="label">  
 <label>Something</label>  
 <file>namespace/module/something.html</file>  
 <type>html</type>  
 </your_module_email_something_template>  
 </email>  
 </template>  
 </global>  
 </config>

———-  
Block Caching

 To cache a block individually, add this method to the blocks class:

 protected function _construct()  
 {  
 $this->addData(array(  
 ‘cache_lifetime’ => 3600,  
 ‘cache_tags’ => array(Mage_Cms_Model_Block::CACHE_TAG),  
 ‘cache_key’ => ‘CACHE_KEY’,  
 ));  
 }

———–  
Config Two-Level Memcached &amp; DB Definition

 <config>  
 <global>  
 <cache>  
 <backend>memcached</backend>  
 <slow_backend>database</slow_backend>  
 <id_prefix>cache_</id_prefix>  
 <memcached>  
 <servers>  
 <server1>  
 <host><![CDATA[localhost]]></host> <port><![CDATA[11211]]></port> <persistent><![CDATA[0]]></persistent> <weight><![CDATA[1]]></weight>  
 <timeout><![CDATA[60]]></timeout>  
 <retry_interval><![CDATA[10]]></retry_interval>  
 </server1>  
 </servers>  
 <compression><![CDATA[0]]></compression>  
 <cache_dir><![CDATA[]]></cache_dir>  
 <hashed_directory_level><![CDATA[]]></hashed_directory_level>  
 <hashed_directory_umask><![CDATA[]]></hashed_directory_umask>  
 <file_name_prefix><![CDATA[]]></file_name_prefix>  
 </memcached>  
 </cache>  
 <full_page_cache>  
 <backend>memcached</backend>  
 <slow_backend>database</slow_backend>  
 <id_prefix>fullpagecache_</id_prefix>  
 <memcached>  
 <servers>  
 <server1>  
 <host><![CDATA[localhost]]></host> <port><![CDATA[11211]]></port> <persistent><![CDATA[0]]></persistent> <weight><![CDATA[1]]></weight>  
 <timeout><![CDATA[60]]></timeout>  
 <retry_interval><![CDATA[10]]></retry_interval>  
 </server1>  
 </servers>  
 <compression><![CDATA[0]]></compression>  
 <cache_dir><![CDATA[]]></cache_dir>  
 <hashed_directory_level><![CDATA[]]></hashed_directory_level>  
 <hashed_directory_umask><![CDATA[]]></hashed_directory_umask>  
 <file_name_prefix><![CDATA[]]></file_name_prefix>  
 </memcached>  
 </full_page_cache>  
 </global>  
 </config>

———–  
Add comment to form input in admin

 $afterElementHtml = ‘

<small>‘ . ‘ this is the hint! ‘ . ‘</small>

‘;

 $linkFieldset->addField(‘field_name’, ‘text’, array(  
 ‘after_element_html’ => $afterElementHtml,  
 ));

———–  
Category Product Collection

 This snippet provides a collection of products within a category

 $cat = Mage::getModel(‘catalog/category’)->load(1);  
 $coll = Mage::getResourceModel(‘catalog/product_collection’);  
 $coll->addCategoryFilter($cat);

———-  
Adding BreadCrumbs

 Via code (usually in a controller):

 $crumbs = Mage::app()->getLayout->getBlock(‘breadcrumbs’);  
 $crumbs->addCrumb(‘home’, array(  
 ‘label’ => ‘Home’,  
 ‘title’ => ‘Go to Home Page’,  
 ‘link’ => Mage::getUrl(”)  
 ));

 Via Layout XML:

 <reference name="breadcrumbs">  
 <action method="addCrumb">  
 <crumbname>Home</crumbname>  
 <crumbinfo>  
 <label>Home</label>  
 <title>Go to Home Page</title> <link></link>/ </crumbinfo>  
 </action>  
 </reference>

———-

Adding new Total Collector Model….

 extends… Mage_Sales_Model_Quote_Address_Total_Abstract  
 config… config/global/sales/quote/totals/custom…

 <config>  
 <global>  
 <sales>  
 <quote>  
 <totals>  
 <custom_total>  
 <class>mynamespace_mymodule/total</class>  
 <before>grand_total</before>  
 <after>subtotal,tax_subtotal</after>  
 </custom_total>  
 </totals>  
 </quote>  
 </sales>  
 </global>  
 </config>

 priority of total collector models can be changed by before and after tags..

 The method *collect* is used to calculate total for the shopping cart, and the method *fetch* is used to fetch data to display in frontend

————–

custom product type..

 xpath: global/catalog/product/type/custom_product_type/model&amp;price_model&amp;allow_product_types&amp;price_indexer  
 <catalog> <product> <type>  
 <configurable module="catalog" translate="label">  
 <label>Configurable Product</label>  
 <model>catalog/product_type_configurable</model> <price_model>catalog/product_type_configurable_price</price_model> <composite>1</composite>  
 <allow_product_types>  
 <simple></simple>  
 <virtual></virtual>  
 </allow_product_types>  
 <index_priority>30</index_priority> <price_indexer>catalog/product_indexer_price_configurable</price_indexer> </configurable>  
 </type> </product> </catalog>

————–

custom indexer..

 xpath: global/index/indexer/custom_indexer/model&amp;depends  
 <config>  
 <global>  
 <index>  
 <indexer>  
 <test_indexer>  
 <model>test/indexer</model>  
 <depends>  
 <catalog_url></catalog_url>  
 </depends>  
 </test_indexer>  
 </indexer>  
 </index>  
 </global>  
 </config>

 class Blah.. extends Mage_Index_Model_Indexer_Abstract  
 getName: get custom indexer name  
 getDescription: get custom indexer description  
 _registerEvent: custom registered event  
 _processEvent: used when processing the index event  
 reindexAll: reindex all items of your entity

 Mage::getModel(‘index/indexer’)->

————–  
Getting A Database Adapter (Read or Write)

 To read:

 Mage::getSingleton(‘core/resource’)->getConnection(‘core_read’);

 To write:

 Mage::getSingleton(‘core/resource’)->getConnection(‘core_write’);

———-  
Add Product attribute

 $installer = Mage::getResourceModel(‘catalog/setup’, ‘catalog_setup’);

 if (!$installer->getAttributeId(Mage_Catalog_Model_Product::ENTITY, ‘attribute_name’)) {

 $installer->addAttribute(Mage_Catalog_Model_Product::ENTITY, ‘attribute_name’, array( // TABLE.COLUMN: DESCRIPTION:

 ‘label’ => ‘Label’, // eav_attribute.frontend_label — admin input label

 ‘group’ => ‘General’, // (not a column) tab in product edit screen

 ‘sort_order’ => 0, // eav_entity_attribute.sort_order sort order in group

 ‘backend’ => ‘module/class_name’, // eav_attribute.backend_model — backend class (module/class_name format)

 ‘type’ => ‘varchar’, // eav_attribute.backend_type — backend storage type (varchar, text etc)

 ‘frontend’ => ‘module/class_name’, // eav_attribute.frontend_model — admin class (module/class_name format)

 ‘note’ => null, // eav_attribute.note — admin input note (shows below input)

 ‘default’ => null, // eav_attribute.default_value — admin input default value

 ‘wysiwyg_enabled’ => false, // catalog_eav_attribute.is_wysiwyg_enabled — (products only) admin input wysiwyg enabled

 ‘input’ => ‘input_name’, // eav_attribute.frontend_input — admin input type (select, text, textarea etc)

 ‘input_renderer’ => ‘module/class_name’, // catalog_eav_attribute.frontend_input_renderer — (products only) admin input renderer  
 (otherwise input is used to resolve renderer)

 ‘source’ => null, // eav_attribute.source_model — admin input source model (for selects) (module/class_name format)

 ‘required’ => true, // eav_attribute.is_required — required in admin

 ‘user_defined’ => false, // eav_attribute.is_user_defined — editable in admin attributes section, false for not

 ‘unique’ => false, // eav_attribute.is_unique — unique value required

 ‘global’ => Mage_Catalog_Model_Resource_Eav_Attribute::SCOPE_GLOBAL, // catalog_eav_attribute.is_global —  
 (products only) scope

 ‘visible’ => true, // catalog_eav_attribute.is_visible — (products only) visible on admin, setting to false stops import  
 of this attribute

 ‘visible_on_front’ => false, // catalog_eav_attribute.is_visible_on_front — (products only) visible on frontend (store)  
 attribute table

 ‘used_in_product_listing’ => false, // catalog_eav_attribute.used_in_product_listing — (products only) made available in  
 product listing

 ‘searchable’ => false, // catalog_eav_attribute.is_searchable — (products only) searchable via basic search

 ‘visible_in_advanced_search’ => false, // catalog_eav_attribute.is_visible_in_advanced_search (products only) searchable via  
 advanced search

 ‘filterable’ => false, // catalog_eav_attribute.is_filterable — (products only) use in layered nav

 ‘filterable_in_search’ => false, // catalog_eav_attribute.is_filterable_in_search — (products only) use in search results  
 layered nav

 ‘comparable’ => false, // catalog_eav_attribute.is_comparable — (products only) comparable on frontend

 ‘is_html_allowed_on_front’ => true, // catalog_eav_attribute.is_visible_on_front — (products only) seems obvious, but also see  
 visible

 ‘apply_to’ => ‘simple,configurable’, // catalog_eav_attribute.apply_to — (products only) which product types to apply to

 ‘is_configurable’ => false, // catalog_eav_attribute.is_configurable — (products only) used for configurable products  
 or not

 ‘used_for_sort_by’ => false, // catalog_eav_attribute.used_for_sort_by — (products only) available in the ‘sort by’ menu

 ‘position’ => 0, // catalog_eav_attribute.position — (products only) position in layered naviagtion

 ‘used_for_promo_rules’ => false, // catalog_eav_attribute.is_used_for_promo_rules — (products only) available for use in  
 promo rules

 ));  
 }

—————  
mage_sales_model_quote  
* Supported events:  
 * sales_quote_load_after  
 * sales_quote_save_before  
 * sales_quote_save_after  
 * sales_quote_delete_before  
 * sales_quote_delete_after

————  
The “->getTypeInstance(true)” allows you to retrieve an object that describes the type of the product, where type is the internal magento type. So, you can use this method to determine if a products is a simple product, a bundled product, a configurable product, etc.  
————

Magento translate trace…

 Mage::helper(‘core’)->__()  
 Mage::app()->getTranslator()  
 Mage_Core_Model_Translate::translate()

————————————————  
Show custom total…

 sales_order_view – frontend order view page  
 sales_order_invoice  
 sales_order_creditmemo

 sales_order_print – print page

 sales_email_order_items – email template  
 sales_email_order_invoice_items  
 sales_email_order_creditmemo_items

 adminhtml_sales_order_view – backend order view page  
 adminhtml_sales_order_invoice_new – backend new invoice view page  
 adminhtml_sales_order_invoice_view – backend invoice view page  
 adminhtml_sales_order_creditmemo_new – backend new creditmemo view page  
 adminhtml_sales_order_creditmemo_view – backend creditmemo view page

————–

Different from catalog cart rules, shopping cart rules define the promotion for customer only when customer checks out product. They can be specified by either coupon code or others.

————–  
http://magento-quickies.tumblr.com/post/14272607486/configurable-product-research  
————–

*catalog_product_super_link* table only contains data related to configurable products.  
*catalog_product_relation* contains the relation information for bundled and grouped products, in addition to the configurable relations.  
*eav_entity_store* contains increment id information of orders, invoices, creditmemos, shipments, etc..  
————–  
*tier prices* works with website, customer group, price and quantity (price_qty).  
————–

admin menu, render navigation items by class Mage_Adminhtml_Block_Page_Menu

_isAllowed() checks navigation permission acl,

User: the entity that has an authority to use the system. The user that we mention in Magento is the backend user.  
Role: the role of the user when logging in to the system. In Magento, a user has only a role.  
Rule: the rule set of user and role. It defines user’s permission or role’s permission to access the resource.  
Assert: the condition to active an item in ACL. It is used for a special control when checking permission by ACL.  
—————-

– Accessing Magento API via SOAP – basic steps

Create appropriate role (Magento Admin)  
Create web services user (Magento Admin)  
Assign created role to the user (Magento Admin)  
Log-in to web service and retrieve Session Id (Soap Client)  
Call appropriate method (Soap Client)

—————–

Different ways to instantiate block:  
 – $block = new Packagename_Modulename_Block_Foo;  
 – $class = Mage::getConfig()->getBlockClassName(‘groupname/foo’);  
 $block = new $class;  
 – $layout = Mage::getSingleton(‘core/layout’);  
 $block = $layout->createBlock(‘groupname/foo’);  
 OR $block = $this->getLayout()->createBlock(‘groupname/foo’);  
 – <block name="baz" type="groupname/foo"></block>

– Call block outside Magento

 require_once ‘app/Mage.php’;  
 Mage::init();

 $layout = Mage::app()->getLayout();  
 $layout->getUpdate()  
 ->addHandle(‘default’)  
 ->addHandle(‘some_other_handle’)  
 ->load();

 /*  
 * Generate blocks, but XML from previously loaded layout handles must be  
 * loaded first.  
 */  
 $layout->generateXml()  
 ->generateBlocks();

 $cart = $layout->getBlock(‘cart_sidebar’)->toHtml();  
 echo $cart;

———-

To create new attribute in customer frontend, these three tables will be affected:

 – eav_attribute  
 – customer_eav_attribute : id of eav_attribute here..  
 – customer_form_attribute : 3 entries here too, for adminhtml_customer, customer_account_create and customer_account_edit

——————–

simple models have a resource that inherits from Mage_Core_Model_Mysql4_Abstract  
EAV models inherits from Mage_Eav_Model_Entity_Abstract

Mage_Eav_Model_Entity_Abstract, there is no _init method  
Mage_Eav_Model_Entity_Abstract :: _construct is not an abstract method

—————-

EAV setup: Mage_Eav_Model_Entity_Setup

//to add in eav_entity_type table…  
$installer->addEntityType(‘complexworld_eavblogpost’, array(  
 //entity_mode is the URI you’d pass into a Mage::getModel() call  
 ‘entity_model’ => ‘complexworld/eavblogpost’,

 //table refers to the resource URI complexworld/eavblogpost  
 //<complexworld_resource>…<eavblogpost></eavblogpost></complexworld_resource>


 ‘table’ =>’complexworld/eavblogpost’,  
));

//to create eav tables for int, varchar, text, datetime, decimal…  
$installer->createEntityTables(  
 $this->getTable(‘complexworld/eavblogpost’)  
);

————-

if you have an order with three items and you refund one item the order don´t change the state, only when you refund all item of the order this change to closed state  
————–

to render a block, Mage_Core_Block_Template::renderView() is called  
to render a block HTML, Mage_Core_Block_Template::_toHtml() is called

—————  
In addAttribute(), if attribute is system, it will add to all existing attribute sets  
—————

in Mage_Adminhtml_Block_Widget_Grid_Container  
$_blockGroup is your module’s name.  
$_controller is the path to your grid block.

————-

Direct SQL queries:

 $resource = Mage::getSingleton(‘core/resource’);  
 $readConnection = $resource->getConnection(‘core_read’);  
 $writeConnection = $resource->getConnection(‘core_write’);

 $tableName = $resource->getTableName(‘catalog_product_entity’);  
 $tableName = $resource->getTableName(‘catalog/product’);

 $readConnection->fetchAll(……

 fetchAll() – Fetches all SQL result rows as a sequential array.  
 fetchCol() – Fetches the first column of all SQL result rows as an array.  
 fetchOne() – Fetches the first column of the first row of the SQL result.  
 fetchRow() – Fetches the first row of the SQL result.  
 fetchAssoc() – Fetches all SQL result rows as an associative array.  
 fetchPairs() – Fetches all SQL result rows as an array of key-value pairs.

———————-

Varien_Db_Adapter_Pdo_Mysql::prepareSqlCondition($fieldname, $condition)

 If $condition integer or string – exact value will be filtered (‘eq’ condition)  
 *  
 * If $condition is array – one of the following structures is expected:  
 * – array(“from” => $fromValue, “to” => $toValue)  
 * – array(“eq” => $equalValue)  
 * – array(“neq” => $notEqualValue)  
 * – array(“like” => $likeValue)  
 * – array(“in” => array($inValues))  
 * – array(“nin” => array($notInValues))  
 * – array(“notnull” => $valueIsNotNull)  
 * – array(“null” => $valueIsNull)  
 * – array(“moreq” => $moreOrEqualValue)  
 * – array(“gt” => $greaterValue)  
 * – array(“lt” => $lessValue)  
 * – array(“gteq” => $greaterOrEqualValue)  
 * – array(“lteq” => $lessOrEqualValue)  
 * – array(“finset” => $valueInSet)  
 * – array(“regexp” => $regularExpression)  
 * – array(“seq” => $stringEqual)  
 * – array(“sneq” => $stringNotEqual)  
 *  
 * If non matched – sequential array is expected and OR conditions  
 * will be built using above mentioned structure

————————-

reindex via code….

 $indexer = Mage::getSingleton(‘index/indexer’);  
 $process = $indexer->getProcessByCode(‘catalog_product_price’);  
 $process->reindexEverything();

 The following are indexer codes which you can use instead of the catalog_product_price index above:

 catalog_product_attribute Product Attributes  
 catalog_product_price Product Prices  
 catalog_url Catalog URL Rewrites  
 catalog_product_flat Product Flat Data  
 catalog_category_flat Category Flat Data  
 catalog_category_product Category Products  
 catalogsearch_fulltext Catalog Search Index  
 cataloginventory_stock Stock Status  
 tag_summary Tag Aggregation Data

————————

Mage::getSingleton(‘core/session’)->addError(‘An Error’);  
Mage::getSingleton(‘core/session’)->addWarning(‘A Warning’);  
Mage::getSingleton(‘core/session’)->addNotice (‘A Notice’);  
Mage::getSingleton(‘core/session’)->addSuccess(‘A Success’);

—————

display “out of stock” uses these indexes:

 Product Attributes (catalog_product_attribute)  
 Product Prices (catalog_product_price)

—————-

Altering Config Data During Setup:

 Setting a value in the default scope:  
 $installer->setConfigData(‘some/path’, ‘value’);

 Setting a value in a specific store:  
 $installer->setConfigData(‘some/path’, ‘value’, ‘stores’, 1);

 Deleting a value from all scopes:  
 $installer->deleteConfigData(‘some/path’);

 Deleting a value from a certain scope (unfortunately you cannot choose which scope ID though:  
 $installer->deleteConfigData(‘some/path’, ‘stores’);

——————-

Clearing cache:

 Clean everything (use either):  
 Mage::app()->getCacheInstance()->flush();  
 Mage::app()->getCache()->clean();

 Clean specific types:  
 Mage::app()->getCacheInstance()->cleanType(‘config’);  
 instead of config, we can use layout, block_html, translate, collections, eav, config_api

——————-

Get all declared cache types:  
 Mage::app()->getCacheInstance()->getTypes();

——————-

source model in backend Adminhtml module, *requires to return* toOptionArray()  
source model in EAV while adding attributes *requires to return* getAllOptions()

The core/template block is the foundation of the template system, allowing us the ability to load .phtml files from our themes.  
The page/html_pager block provides generic methods for paginating collections, such as isLastPage().  
cron/observer::dispatch handles the cron schedule’s creation, cleanup and execution of the jobs defined in the various config.xml files

—————-

required fields when creating a new category in backend:

name, is_active, include_in_menu, available_sort_by, default_sort_by

required fields when creating a new product in backend:

name, sku, weight, status, visibility, tax class, price, short_desc, description, qty  
—————–

The shipping rate is upon Weight vs. Destination, Price vs. Destination, or # of Items vs. Destination (site admin can configurate for that)

—————–

Mage_Shipping_Model_Carrier_Abstract:: collectRates()  
Mage_Shipping_Model_Carrier_Interface:: isTrackingAvailable(), getAllowedMethods()

————-

while adding new attributes in $setup->addAttribute(‘order’, …

| catalog_category |  
| catalog_product |  
| creditmemo |  
| creditmemo_comment |  
| creditmemo_item |  
| customer |  
| customer_address |  
| customer_payment |  
| invoice |  
| invoice_comment |  
| invoice_item |  
| invoice_shipment |  
| order |  
| order_address |  
| order_item |  
| order_payment |  
| order_status |  
| order_status_history |  
| quote |  
| quote_address |  
| quote_address_item |  
| quote_address_rate |  
| quote_item |  
| quote_payment |  
| shipment |  
| shipment_comment |  
| shipment_item |  
| shipment_track |

———————————-

Adding JS, Skin JS and CSS files…

 <action method="addItem"><type>skin_js</type><name>js/ie6.js</name><params></params><if>lt IE 7</if></action>  
 <action method="addItem"><type>js</type><name>lib/ds-sleight.js</name><params></params><if>lt IE 7</if></action>  
 <action method="addItem"><type>skin_css</type><name>css/styles-ie.css</name><params></params><if>lt IE 8</if></action>  
 <action method="addJs"><script>mage/cookies.js</script></action>  
 <action method="addCss"><stylesheet>css/print.css</stylesheet><params>media=”print”</params></action>

———–

CMS Directives…..

 can be used in CMS, static blocks or emails

 {{block id=’block_id’}}  
 {{block type=’module/package_classname’ template=’path/to/template.phtml’}}  
 {{config path=’section/group/field’}}  
 {{htmlescape var=” allowed_tags=”}}  
 {{htmlescape var=’[Hello](javascript:alert(1);)‘}}  
 //this outputs [Hello](javascript:alert(1);) and doesn’t interpreted by browsers  
 {{layout handle=”}}  
 {{media url=”}}  
 {{skin url=”}}  
 {{store url=”}}

 {{block type=’namespace_custom/test’ my_param1=’value 1′ my_param2=’value 2′}}

{{< /highlight >}}

BEST LUCK! :)

</theme></package>