---
id: 247
title: 'Magento: Difference between source_model, frontend_model, backend_model'
date: '2012-04-15T07:15:06+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento Interview'
tags:
    - backend_model
    - difference
    - frontend_model
    - magento
    - source_model
    - versus
---

When dealing with Magento Admin’s system configuration, you may have encountered with these models. If you don’t know, these models are used when you add custom fields through your system.xml file at Magento’s backend configuration (Admin -> System -> Configuration).

Okay, so the difference between these 3 models are:

**source_model**:  
It specifies a Model class, where you will be returned with options that can populate in the current field.

Example,  
{{< highlight php "style=emacs" >}}<source_model>adminhtml/system_config_source_yesno</source_model>{{< /highlight >}}  
this will populate select dropdown with values Yes/No

**frontend_model**:  
It specifies a Block class to add custom render to use as a frontend field type instead of/along with default frontend_type field value (text, textarea, select, etc.).

Example,  
{{< highlight xml "style=emacs" >}}<frontend_type>button</frontend_type>  
<frontend_model>MyCustomModule/button</frontend_model>{{< /highlight >}}  
this will keep frontend type as button, but the customized one taken from Block class Button.php of MyCustomModule module

Code at Button.php can be anything like this:  
{{< highlight php "style=emacs" >}}<?php class MyNamespace_MyCustomModule_Block_Button extends Mage_Adminhtml_Block_System_Config_Form_Field
{

    protected function _getElementHtml(Varien_Data_Form_Element_Abstract $element)
    {
        $this->
setElement($element);  
 $url = $this->getUrl(‘catalog/product’);

 $html = $this->getLayout()->createBlock(‘adminhtml/widget_button’)  
 ->setType(‘button’)  
 ->setClass(‘scalable’)  
 ->setLabel(‘Run Now !’)  
 ->setOnClick(“setLocation(‘$url’)”)  
 ->toHtml();

 return $html;  
 }  
}  
?>{{< /highlight >}}

**backend_model**:  
Generally, when you save any form at System Configuration, the data is stored in the table core_config_data. But if your requirement is to do something prior/after the save is performed, you can do it by having _beforeSave() &amp; _afterSave() methods defined in this custom/defined class.

Example,  
{{< highlight xml "style=emacs" >}}<backend_model>adminhtml/system_config_backend_shipping_tablerate</backend_model>{{< /highlight >}}