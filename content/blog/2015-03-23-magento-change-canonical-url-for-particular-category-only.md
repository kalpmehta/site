---
id: 985
title: 'Magento: Change canonical URL for particular category only'
date: '2015-03-23T18:46:40+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=985'
permalink: /index.php/2015/03/23/magento-change-canonical-url-for-particular-category-only/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2014/06/22/magento-sample-apache-virtualhost-for-your-website/"     class="crp_title">Magento: Sample apache virtualhost for your website</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-delete-empty-categories-and-sub-categories/"     class="crp_title">Magento delete empty categories and sub-categories</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li></ul></div>'
crp_related_posts_feed:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2014/06/22/magento-sample-apache-virtualhost-for-your-website/"     class="crp_title">Magento: Sample apache virtualhost for your website</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-performace-optimization-catalog-url-rewrite-management/"     class="crp_title">Magento performace optimization, Catalog URL Rewrite Management</a></li><li><a href="http://ka.lpe.sh/2013/08/17/magento-delete-empty-categories-and-sub-categories/"     class="crp_title">Magento delete empty categories and sub-categories</a></li></ul><div class="crp_clear"></div></div>'
categories:
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