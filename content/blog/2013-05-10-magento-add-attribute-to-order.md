---
id: 604
title: 'Magento add attribute to order'
date: '2013-05-10T21:46:48+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - attribute
    - magento
    - order
---

Adding custom attribute to order in Magento is same as we do for customer and category. The difference is we will use different setup class AND we will not need attribute set, group and attribute input type now. We will create a quick module which will do exactly what we want and nothing more than that. So let’s start our new module.

1.) Create a file at app/etc/modules/ and name it whatever you want. I will name it Namespace_Module.xml  
Paste this code in that file:  
{{< highlight xml "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <namespace_module>  
 <active>true</active>  
 <codepool>local</codepool>  
 </namespace_module>  
 </modules>  
</config>{{< /highlight >}}

2.) Create necessary directories to reach to app/code/local/Namespace/Module/etc/, so that we can create our config.xml there. Paste below code in this config file:  
{{< highlight xml "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <namespace_module>  
 <version>0.0.1</version>  
 </namespace_module>  
 </modules></config>

 <global>  
 <resources>  
 <modulename_setup>  
 <setup>  
 <module>Namespace_Module</module>  
 <class>Mage_Sales_Model_Mysql4_Setup</class>  
 </setup>  
 <connection>  
 <use>core_setup</use>  
 </connection>  
 </modulename_setup>  
 <modulename_write>  
 <connection>  
 <use>core_write</use>  
 </connection>  
 </modulename_write>  
 <modulename_read>  
 <connection>  
 <use>core_read</use>  
 </connection>  
 </modulename_read>  
 </resources>  
 </global>  
{{< /highlight >}}  
  
3.) Now comes our main file, which will create new Order attribute for us. Create file “mysql4-install-0.0.1.php” in app/code/local/Namespace/Module/sql/module_setup/, and paste the below code in it:  
{{< highlight php "style=emacs" >}}<?php $this->
startSetup();  
$this->addAttribute(‘order’, ‘your_custom_attribute_here’, array(  
 ‘type’ => ‘varchar’,  
 ‘label’ => ‘Custom Order attribute label’,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘visible_on_front’ => true,  
 ‘user_defined’ => true  
));

$this->endSetup();{{< /highlight >}}

This will add new attribute to Order and after clearing cache you can see your custom attribute in backend “Manage Orders” screen and in customer frontend screen “My Orders”. HTH!