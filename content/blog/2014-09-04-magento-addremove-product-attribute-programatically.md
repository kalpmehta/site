---
id: 932
title: 'Magento add/remove product attribute programatically'
date: '2014-09-04T02:24:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=932'
permalink: /index.php/2014/09/04/magento-addremove-product-attribute-programatically/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/"     class="crp_title">Magento: Add customer Facebook, Twitter, Google+, Pinterest handles</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-options/"     class="crp_title">Magento get attribute options</a></li></ul></div>'
categories:
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