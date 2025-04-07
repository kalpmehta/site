---
id: 447
title: 'Magento: Add product custom attribute options dynamically'
date: '2013-02-07T16:19:00+00:00'
author: kalpesh
layout: post
tags:
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