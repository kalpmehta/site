---
id: 247
title: 'Magento: Difference between source_model, frontend_model, backend_model'
date: '2012-04-15T07:15:06+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=247'
permalink: /index.php/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li><li><a href="http://ka.lpe.sh/2012/07/12/magento-add-radio-checkbox-button-to-admin-grid/"     class="crp_title">Magento add radio / checkbox button to admin grid</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li></ul></div>'
categories:
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