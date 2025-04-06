---
id: 447
title: 'Magento: Add product custom attribute options dynamically'
date: '2013-02-07T16:19:00+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=447'
permalink: /index.php/2013/02/07/magento-add-product-custom-attribute-options-dynamically/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'insert attribute options programatically'
    - 'magento dynamically add product attribute options'
    - 'product attribute options installer'
---

Once you have the product attributes in place, and you want to add lot of options to these attributes it becomes time consuming and hectic task. If you have only few attribute options to add, it’s easy to go to backend and add manually. But if you have many attribute options, more than 10 options for many attributes, it’s very tiresome and feels like data entry job. Magento is not built to do stuff manually, so here I will provide you the code snippet which will push all the attribute options to their respective attribute.

Create a file in the root of your Magento installation and copy this code there. I generally name it test.php  
{{< highlight php "style=emacs" >}}require_once ‘app/Mage.php’;  
umask(0);  
Mage::app(‘default’);

$installer = new Mage_Eav_Model_Entity_Setup(‘core_setup’);  
$installer->startSetup();

//Change this….  
$aColors = array(‘PINK’,’BLACK’,’BLUE’,’BROWN’,’GOLD’,’GRAY’,’GREEN’,’MULTI’,’NEUTRALS/CREAM/WHITE’,’ORANGE’,’PURPLE’,’RED’,’RUST’,’TAUPE’,’YELLOW’);  
$attrCode = ‘color’; //this should be there already  
//……..

$aColors = array_map(‘utf8_encode’,$aColors); //If you’re using special characters  
$iProductEntityTypeId = Mage::getModel(‘catalog/product’)->getResource()->getTypeId();  
$aOption = array();  
$aOption[‘attribute_id’] = $installer->getAttributeId($iProductEntityTypeId, $attrCode);

for($iCount=0;$iCount<sizeof>addAttributeOption($aOption);</sizeof>

$installer->endSetup();{{< /highlight >}}  
Now you just need to give the **existing** product attribute name AND **future** attribute options to this script. Run it and rest all script will do for you! 🙂