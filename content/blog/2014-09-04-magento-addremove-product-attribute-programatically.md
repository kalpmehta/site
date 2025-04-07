---
id: 932
title: 'Magento add/remove product attribute programatically'
date: '2014-09-04T02:24:16+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - attribute
    - magento
    - product
---

Magento add product attribute using sql setup file in your module. Also assign your custom attribute to attribute set Default and group General programatically.

Below code will add your new attribute in Manage Products edit screen at the end of General tab with dropdown values Yes/No. It will not display in frontend website but you can change visibible on front to 1 if you wish. Note that it will assign to Default attribute set only but you can change it to whatever as per your requirement.

{{< highlight php "style=emacs" >}}  
$model = Mage::getResourceModel(‘catalog/setup’,’catalog_setup’);

$data=array(  
‘type’=>’int’,  
‘input’=>’boolean’, //for Yes/No dropdown  
‘sort_order’=>50,  
‘label’=>’CUSTOM ATTRIBUTE CODE LABEL’,  
‘global’=>Mage_Catalog_Model_Resource_Eav_Attribute::SCOPE_GLOBAL,  
‘required’=>’0’,  
‘comparable’=>’0’,  
‘searchable’=>’0’,  
‘is_configurable’=>’1’,  
‘user_defined’=>’1’,  
‘visible_on_front’ => 0, //want to show on frontend?  
‘visible_in_advanced_search’ => 0,  
‘is_html_allowed_on_front’ => 0,  
‘required’=> 0,  
‘unique’=>false,  
‘apply_to’ => ‘configurable’, //simple,configurable,bundled,grouped,virtual,downloadable  
‘is_configurable’ => false  
);

$model->addAttribute(‘catalog_product’,’CUSTOM_ATTRIBUTE_CODE’,$data);

$model->addAttributeToSet(  
 ‘catalog_product’, ‘Default’, ‘General’, ‘CUSTOM_ATTRIBUTE_CODE’  
); //Default = attribute set, General = attribute group  
{{< /highlight >}}

To remove the product attribute using the setup file, use below code instead:

{{< highlight php "style=emacs" >}}  
$model = Mage::getResourceModel(‘catalog/setup’,’catalog_setup’);  
$model->removeAttribute(‘catalog_product’,’CUSTOM_ATTRIBUTE_CODE’);  
{{< /highlight >}}