---
id: 1012
title: 'Magento: Zipcode + 4 tax calculation bug fix'
date: '2015-09-04T05:39:10+00:00'
author: kalpesh
layout: post
tags:
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