---
id: 825
title: 'Magento convert attribute type from TEXT to DROPDOWN'
date: '2013-08-13T23:15:44+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=825'
permalink: /index.php/2013/08/13/magento-convert-attribute-type-from-text-to-dropdown/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"367424293522931712";s:5:"pDate";s:19:"2013-08-13 23:15:52";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/07/magento-add-product-custom-attribute-options-dynamically/"     class="crp_title">Magento: Add product custom attribute options dynamically</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-options/"     class="crp_title">Magento get attribute options</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-value/"     class="crp_title">Magento get attribute value</a></li><li><a href="http://ka.lpe.sh/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/"     class="crp_title">Magento: Get all the values of a Magento EAV for a particular attribute code</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-attribute-label/"     class="crp_title">Magento get attribute label</a></li></ul></div>'
snap_isAutoPosted:
    - '1'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5773190272091435008&amp;type=U&amp;a=aHBE";s:5:"pDate";s:19:"2013-08-13 23:17:01";}}";'
categories:
    - Magento
    - 'Magento admin'
tags:
    - attribute
    - magento
---

Magento convert attribute type from TEXT (varchar) to DROPDOWN / SELECT (int) in Backend.  
Magento doesn’t have this in-built so we will have to do it in our own way. We will convert our existing attribute which is in TEXT type, to DROPDOWN (select). Let’s say our attribute code is “vendor”, you will need to replace it with your own attribute code in all the code below.

**WARNING**: All the coupon codes that uses this attribute for discounts/promotions will GO AWAY! Please note down all the coupon code Conditions and Actions (which uses this attribute) before converting the attribute.

**Step 1.)** Backup your database.  
{{< highlight mariadb "style=emacs" >}}mysqldump -u mysqluser -p mysqldbname > mysqldbname_backup.sql{{< /highlight >}}

**Step 2.)** Export all the values of the attribute you want to convert in a CSV file. For that, create a file vendor.php (your_attribute.php) in your magento root with following code inside it:  
{{< highlight php "style=emacs" >}}require “app/Mage.php”;  
umask(0);  
Mage::app();

$collection = Mage::getModel(‘catalog/product’)  
 ->getCollection()  
 ->addAttributeToSelect(‘sku’)  
 ->addAttributeToSelect(‘vendor’); //replace vendor with your attribute code

$data = $collection->getData();

foreach ($data as $product) {  
 echo $product[‘entity_id’] . “,” . $product[‘vendor’].”\\n”;  
}{{< /highlight >}}

After saving the above code, run it from command line:

{{< highlight http >}} php vendor.php > vendor.csv{{< /highlight >}}  
You should now have all the attribute’s data with product ID in the vendor.csv (your_attribute.csv) file.

**Step 3.)** Now get all the unique values you have in the attribute’s data, which we will be filling them as options of select dropdown.  
Run following mysql command to get all the unique values and copy them in a new file:  
{{< highlight mariadb "style=emacs" >}}select distinct value from catalog_product_entity_varchar where attribute_id in (select attribute_id from eav_attribute where attribute_code=’vendor’); //replace vendor with your own attribute code{{< /highlight >}}

After this step, we have all the attribute’s data in CSV file, and all the UNIQUE attribute values.  
  
**Step 4.)** Note all the settings of the attribute and Delete the attribute from backend Manage Attributes screen. Now create new attribute from there with SAME attribute code but different Frontend Type (Dropdown). Rest all the settings will be same as you had it before. Save it. Go to Manage Attribute Sets page and assign the attribute to the Group it was assigned to before.

**Step 5.)** Now we have to insert all the options to this attribute so that the values are shown in the dropdown. Edit your vendor.php file and replace the code with below:  
{{< highlight php "style=emacs" >}}require “app/Mage.php”;  
umask(0);  
Mage::app();

$installer = new Mage_Eav_Model_Entity_Setup(‘core_setup’);  
$installer->startSetup();

//Change this….  
$values = array(“val1″,”val2”); //your unique attributes values that you copied in a new file  
$attrCode = ‘vendor’; //your attribute code here  
//……..

$values = array_map(‘utf8_encode’,$values); //If you’re using special characters  
$iProductEntityTypeId = Mage::getModel(‘catalog/product’)->getResource()->getTypeId();  
$aOption = array();  
$aOption[‘attribute_id’] = $installer->getAttributeId($iProductEntityTypeId, $attrCode);  
for($iCount=0;$iCount<sizeof>addAttributeOption($aOption);</sizeof>

$installer->endSetup();{{< /highlight >}}

After running this, check your attribute manage page and see if all the values are updated or not. You can find the values in “Manage Labels/Options” tab of attribute’s Manage Attributes screen.

**Step 6.)** Now comes the main part which will insert the attribute values in the database. The old values are stored in catalog_product_entity_varchar (text type), while now the values should go to catalog_product_entity_int (dropdown type). Replace your vendor.php file with below code:

{{< highlight php "style=emacs" >}}require “app/Mage.php”;  
umask(0);  
Mage::app();

$attribute = Mage::getModel(‘eav/config’)->getAttribute(‘catalog_product’, ‘vendor’); //change to your attribute code  
$allOptions = $attribute->getSource()->getAllOptions(true, true);  
foreach ($allOptions as $instance) {  
 $myArray[$instance[‘label’]] = $instance[‘value’];  
}

if (($handle = fopen(“vendor.csv”, “r”)) !== FALSE) { //change to your attribute .csv file  
 while (($data = fgetcsv($handle, 1000, “,”)) !== FALSE) {  
 list($_id, $_value) = $data;

 $product = Mage::getModel(‘catalog/product’)->load($_id);  
 $product->setVendor($myArray[$_value]); //setVendor should be setYourAttributeCode

 try {  
 $product->getResource()->saveAttribute($product, ‘vendor’); //change to your attribute code  
 } catch(Exception $e) {  
 echo $_id .”:”. $e->getMessage() .”\\n”;  
 }  
 }  
 fclose($handle);  
}{{< /highlight >}}

Run the file, it will take time to complete depending on how many values you had for that attribute.

**Step 7.)** Clear cache, Re-index the indexes.

Done!  
Test it thoroughly.  
Based on my Magento Stackexchange question: <http://magento.stackexchange.com/questions/6707/convert-attribute-type-from-text-to-dropdown/6710>