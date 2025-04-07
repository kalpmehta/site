---
id: 985
title: 'Magento: Change canonical URL for particular category only'
date: '2015-03-23T18:46:40+00:00'
author: kalpesh
layout: post

tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'canonical url'
    - category
    - 'custom canonical'
    - magento
---

In Magento, if you want to change canonical URL for just one category or quite a few categories, and don’t want to affect rest of the canonical URLs then do the following.

Note that this is helpful when you already have canonical URL in the page and want to REPLACE it with new url. If you don’t have canonical URL at all then you might want to ignore the first *action* tag in the below code.

– Go to the category page you want to change canonical URL in Magento Admin  
– Click the tab “Custom Design”  
– In the Custom Layout Update textbox, paste this:

{{< highlight xml "style=emacs" >}}<reference name="head">  
 <action block="head" method="removeItem">  
 <item>link_rel</item>  
 <name>http://loca.lho.st/old-canonical-url</name>  
 </action>  
 <action method="addLinkRel" translate="title">  
 <rel>canonical</rel>  
 <href>http://loca.lho.st/new-canonical-url</href> </action>  
</reference>{{< /highlight >}}

Change *http://loca.lho.st/old-canonical-url* and *http://loca.lho.st/new-canonical-url* with your desired URLs and save the category.

Basically first *action* tag in the code removes old canonical URL and second *action* tag adds the canonical URL with the new value you specify.

You may also need to clear cache.

HTH!