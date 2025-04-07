---
id: 905
title: 'Magento get State Code, ID, Name from Region ID'
date: '2014-06-25T05:26:30+00:00'
author: kalpesh
layout: post
tags:
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