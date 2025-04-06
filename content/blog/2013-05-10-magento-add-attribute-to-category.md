---
id: 599
title: 'Magento add attribute to category'
date: '2013-05-10T21:16:55+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=599'
permalink: /index.php/2013/05/10/magento-add-attribute-to-category/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/"     class="crp_title">Magento: Add customer Facebook, Twitter, Google+, Pinterest handles</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - attribute
    - category
    - magento
---

Adding category attribute in Magento is same as we add for product and customer. Here in this post I will create a custom module which will add your new custom category attribute in Magento. So let’s start with the module:

1.) As usual, create an XML file in app/etc/modules/ directory, I will name it Namespace_Module.xml  
Paste below code in it changing the Namespace and Module as you want.  
{{< highlight xml "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <namespace_module>  
 <active>true</active>  
 <codepool>local</codepool>  
 </namespace_module>  
 </modules>  
</config>{{< /highlight >}}

2.) Second step would be to create a file config.xml in app/code/local/Namespace/Module/etc/ directory. Create all the directories required get there. Paste the below code in it making sure you have changed Namespace and Module with your naming.  
{{< highlight php "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <namespace_module>  
 <version>0.0.1</version>  
 </namespace_module>  
 </modules></config>

 <global>  
 <resources>  
 <module>  
 <setup>  
 <module>Namespace_Module</module>  
 <class>Mage_Catalog_Model_Resource_Eav_Mysql4_Setup</class>  
 </setup>  
 <connection>  
 <use>core_setup</use>  
 </connection>  
 </module>  
 <module_write>  
 <connection>  
 <use>core_write</use>  
 </connection>  
 </module_write>  
 <module_read>  
 <connection>  
 <use>core_read</use>  
 </connection>  
 </module_read>  
 </resources>  
 </global>  
{{< /highlight >}}  
I have only included setup class and connections as those are the only things we will need to execute our script which will insert the custom attribute to category in our Magento project.  
  
3.) Here comes main file, which will actually add attribute to category. We will put below code in app/code/local/Namespace/Module/sql/module_setup/mysql4-install-0.1.0.php  
{{< highlight php "style=emacs" >}}<?php $this->
startSetup();  
$this->addAttribute(‘catalog_category’, ‘your_custom_attribute_here’, array(  
 ‘group’ => ‘General’,  
 ‘input’ => ‘text’,  
 ‘type’ => ‘varchar’,  
 ‘label’ => ‘Custom Category attribute label’,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘visible_on_front’ => true,  
 ‘global’ => Mage_Catalog_Model_Resource_Eav_Attribute::SCOPE_GLOBAL,  
));

$this->endSetup();  
?>{{< /highlight >}}

We have used minimal things to create this module and add attribute to category. You can go further and do more additions from this.

After clearing cache, you will see that your new custom attribute appear in Category pages in frontend as well as Manage Categories section in backend. HTH!