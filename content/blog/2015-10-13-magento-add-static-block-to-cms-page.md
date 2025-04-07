---
id: 1021
title: 'Magento add static block to cms page'
date: '2015-10-13T21:02:30+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
---

You can add static block to CMS page in Magento in following 2 ways:

1.) By adding code in Layout Update XML of CMS page:  
{{< highlight xml "style=emacs" >}}<reference name="left">  
 <block name="block_name_anything" type="cms/block">  
 <action method="setBlockId">  
 <block_id>STATIC_BLOCK_ID_HERE</block_id>  
 </action>  
 </block>  
</reference>{{< /highlight >}}

2.) By putting below code directly into CMS Page content area:  
{{< highlight http >}} {{block type=”cms/block” block_id=”STATIC_BLOCK_ID_HERE”}}{{< /highlight >}}

Make sure you flush Blocks HTML Output cache if your changes do not reflect on website.