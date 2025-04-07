---
id: 596
title: 'Magento add attribute to customer'
date: '2013-05-10T20:52:55+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - attribute
    - customer
    - magento
---

In Magento to add an attribute to customer is not an option in the admin panel like it does have for Product attribute. So you have to end up writing the script that will add your custom attribute in customer’s EAV tables.

Below code will insert your custom customer attribute in Magento system. You can even specify whil creating the attribute whether that attribute should appear in the forms (like register/signup) or not.

{{< highlight php "style=emacs" >}}$installer = $this;  
$installer->startSetup();

$setup = new Mage_Eav_Model_Entity_Setup(‘core_setup’);

$entityTypeId = $setup->getEntityTypeId(‘customer’);  
$attributeSetId = $setup->getDefaultAttributeSetId($entityTypeId);  
$attributeGroupId = $setup->getDefaultAttributeGroupId($entityTypeId, $attributeSetId);

$setup->addAttribute(‘customer’, ‘your_attribute_code_here’, array(  
 ‘input’ => ‘text’, //or select or whatever you like  
 ‘type’ => ‘int’, //or varchar or anything you want it  
 ‘label’ => ‘Attribute description goes here’,  
 ‘visible’ => 1,  
 ‘required’ => 0, //mandatory? then 1  
 ‘user_defined’ => 1,  
));

$setup->addAttributeToGroup(  
 $entityTypeId,  
 $attributeSetId,  
 $attributeGroupId,  
 ‘your_attribute_code_here’,  
 ‘100’  
);

$oAttribute = Mage::getSingleton(‘eav/config’)->getAttribute(‘customer’, ‘your_attribute_code_here’);  
$oAttribute->setData(‘used_in_forms’, array(‘adminhtml_customer’));  
$oAttribute->save();

$setup->endSetup();{{< /highlight >}}

Here we have used our custom attribute’s:  
– *input* type as *text*, but you can have it anything you like to appear in the form. It can be textarea, date, select or anything you want.  
– data *type* as *int*, but you can have it anything from text, datetime, varchar or decimal. Remember customer is EAV in Magento, so it needs this information to store all the future values of this attribute in customer_entity_int (customer_entity_*) table.