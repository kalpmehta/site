---
id: 53
title: 'Override/Rewrite Magento core blocks and controllers'
date: '2011-06-08T06:23:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=53'
permalink: /index.php/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - block
    - controller
    - magento
---

After spending many hours in rewriting block and controller of Magento core module, I finally came up with a solution.  
Here I am going to rewrite block: **Mage/Adminhtml/Block/Sales/Shipment/Grid.php**  
and controller: **Mage/Adminhtml/controllers/Sales/ShipmentController.php**

First you will need to make a xml file for your new module at app/etc/modules directory  
**CompanyName_Adminhtml.xml**

{{< highlight php "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <companyname_adminhtml>  
 <active>true</active>  
 <codepool>local</codepool>  
 </companyname_adminhtml>  
 </modules>  
</config>{{< /highlight >}}

Then, make folders in your app/code/local directory as follows:  
– CompanyName  
 -> Block  
 —> Sales  
 —-> Shipment  
 ——> Grid.php  
 -> controllers  
 —> Sales  
 —-> ShipmentController.php  
 -> etc  
 —> config.xml

In **etc/config.xml**, your code should look like below:

{{< highlight php "style=emacs" >}}<?xml version="1.0"??>
  
<config>  
 <modules>  
 <companyname_adminhtml>  
 <version>0.1.0</version>  
 </companyname_adminhtml>  
 </modules></config>

 <global>  
 <blocks>  
 <adminhtml>  
 <rewrite>  
 <sales_shipment_grid>CompanyName_Adminhtml_Block_Sales_Shipment_Grid</sales_shipment_grid>  
 </rewrite>  
 </adminhtml>  
 </blocks></global>

 <routers>  
 <adminhtml>  
 <rewrite>  
 <sales_shipment>  
 <from><![CDATA[#^/admin/sales_shipment/$#]]></from>  
 <to>/admin/sales_shipment/</to>  
 </sales_shipment>  
 </rewrite>  
 </adminhtml>  
 </routers>

 <admin>  
 <routers>  
 <adminhtml>  
 <args>  
 <modules>  
 <companyname_adminhtml before="Mage_Adminhtml">CompanyName_Adminhtml</companyname_adminhtml>  
 </modules>  
 </args>  
 </adminhtml>  
 </routers>  
 </admin>

  
{{< /highlight >}}

In **ShipmentController.php**, you should start like this:

{{< highlight php "style=emacs" >}}require_once(“Mage/Adminhtml/controllers/Sales/ShipmentController.php”);  
class CompanyName_Adminhtml_Sales_ShipmentController extends Mage_Adminhtml_Sales_ShipmentController  
{  
 //controller methods goes here..  
}{{< /highlight >}}

require_once is necessary as magento is not going to load controllers as it does for blocks and models

In block **Grid.php**, start the file like below:  
{{< highlight php "style=emacs" >}}class CompanyName_Adminhtml_Block_Sales_Shipment_Grid extends Mage_Adminhtml_Block_Widget_Grid  
{  
 // block methods goes here..  
}{{< /highlight >}}

That’s it! Now you should get your local Grid.php and ShipmentController.php loading instead of core’s.