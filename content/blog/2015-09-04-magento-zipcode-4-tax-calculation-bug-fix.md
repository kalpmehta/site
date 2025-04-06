---
id: 1012
title: 'Magento: Zipcode + 4 tax calculation bug fix'
date: '2015-09-04T05:39:10+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1012'
permalink: /index.php/2015/09/04/magento-zipcode-4-tax-calculation-bug-fix/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2014/10/07/magento-code-already-exists-fix/"     class="crp_title">Magento fix for error &#8220;Code already exists.&#8221;</a></li><li><a href="http://ka.lpe.sh/2015/03/20/magento-incorrect-sales-order-report-dst/"     class="crp_title">Magento bug: Incorrect sales order report during DST</a></li><li><a href="http://ka.lpe.sh/2014/11/07/magento-error-scp-404-get-sppajax___siducoid460pid123/"     class="crp_title">Magento error: SCP 404: GET /spp/ajax/?___SID=Uco/?id=460&#038;pid=123</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - bug
    - calculation
    - magento
    - tax
---

Magento bug fix for zipcode + 4 in tax calculation

Tax Calculation in Magento has a bug where customer can escape paying tax if they enter zipcode + 4 digit in USA. This is because you import 5 digit zipcodes with their tax rates in Magento admin, so if customer inputs their zipcode in zipcode+4 format their zipcode will not match with the imported one. Importing 5-digit zipcode ending in wildcard (*) does not solve this issue either.

Before this fix: If zipcode 90036 collects tax, 90036-1234 does NOT collect tax.

You can fix this bug by adding below code in your custom module:

config.xml  
{{< highlight http >}} …  
<global>  
 <models>  
 <tax_resource>  
 <rewrite>  
 <calculation>Namespace_Module_Model_Tax_Resource_Calculation</calculation>  
 </rewrite>  
 </tax_resource>  
 </models>  
</global>  
…{{< /highlight >}}

Note that we are rewriting core logic of Tax Calculation. Now create folder structure in your custom module: app/code/local/Namespace/Module/Model/Tax/Resource/Calculation.php and copy below code:

{{< highlight http >}} <?php class Namespace_Module_Model_Tax_Resource_Calculation extends Mage_Tax_Model_Resource_Calculation
{
    protected function _getRates($request)
    {
        $countryId = $request->
getCountryId();  
 $regionId = $request->getRegionId();  
 $postcode = $request->getPostcode();

 //12 = california, 25 = iowa  
 if($countryId == ‘US’ &amp;&amp; in_array($regionId,array(12,25))) {  
 $postcode = substr(trim($request->getPostcode()),0,5);  
 $request->setPostcode($postcode);  
 }  
 return parent::_getRates($request);

 }

}{{< /highlight >}}

Above code will only take first 5 digits from the zipcode if the country is USA and state selected is either California or Iowa. You can change the states as per your requirement, to know what ID relates to different states you can look at the State/Province dropdown source code in checkout page.