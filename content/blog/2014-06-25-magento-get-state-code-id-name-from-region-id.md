---
id: 905
title: 'Magento get State Code, ID, Name from Region ID'
date: '2014-06-25T05:26:30+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=905'
permalink: /index.php/2014/06/25/magento-get-state-code-id-name-from-region-id/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:174:"a:1:{i:0;a:4:{s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:4:"doLI";i:0;}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/04/21/magento-order-state-vs-status/"     class="crp_title">Magento: Difference between order states and statuses</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li><li><a href="http://ka.lpe.sh/2013/06/29/magento-get-store-information/"     class="crp_title">Magento get store information</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-get-subcategories-of-a-category/"     class="crp_title">Magento get subcategories of a category by category ID</a></li></ul></div>'
categories:
    - Magento
tags:
    - magento
    - region
    - state
---

Magento get state name, ID, code from region ID or region code.

Get state code from state id

{{< highlight php "style=emacs" >}}$region = Mage::getModel(‘directory/region’)->load(12);  
$state_code = $region->getCode(); //CA{{< /highlight >}}

Get state name from state id

{{< highlight php "style=emacs" >}}$region = Mage::getModel(‘directory/region’)->load(12);  
$state_name = $region->getName(); //California{{< /highlight >}}

Get state id from state code

{{< highlight php "style=emacs" >}}$region = Mage::getModel(‘directory/region’)->loadByCode(‘CA’, ‘US’);  
$state_id = $region->getId(); //12{{< /highlight >}}