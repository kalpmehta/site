---
id: 179
title: 'Magento: Mysql records with NULL values are not fetched in query'
date: '2012-01-08T09:23:13+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=179'
permalink: /index.php/2012/01/08/magento-mysql-records-null-values-not-getting-fetched/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/12/magento-add-admin-user-in-mysql/"     class="crp_title">Magento add admin user in MySQL</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li></ul></div>'
categories:
    - Magento
tags:
    - 'is null'
    - magento
    - 'magento orm'
    - 'query is null'
---

After banging my head on my desk trying to get the records with NULL values with Magento ORM, it was found that writing  
{{< highlight php "style=emacs" >}}$collection->addAttributeToFilter(‘somefield’, ‘null’)  
$collection->addAttributeToFilter(‘somefield’, array(‘is’ => ‘null’)){{< /highlight >}}  
will check for any blank values like this: *WHERE somefield = ”*

So if you want to fetch records that have NULL values in Magento style, you need to write as following:  
{{< highlight php "style=emacs" >}}$collection->addAttributeToFilter(‘somefield’, array(‘null’=>’null’){{< /highlight >}}  
will check like *WHERE somefield = null*

Hope this saves someone’s time!