---
id: 1021
title: 'Magento add static block to cms page'
date: '2015-10-13T21:02:30+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1021'
permalink: /index.php/2015/10/13/magento-add-static-block-to-cms-page/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2015/03/23/magento-change-canonical-url-for-particular-category-only/"     class="crp_title">Magento: Change canonical URL for particular category only</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2014/09/23/magento-show-gift-card-details-in-admin-order-page/"     class="crp_title">Magento: Show gift card details in admin order page</a></li><li><a href="http://ka.lpe.sh/2014/01/05/magento-display-categories-subcategories/"     class="crp_title">Magento display categories and sub-categories</a></li><li><a href="http://ka.lpe.sh/2014/08/22/magento-get-cms-page-content-without-header-footer/"     class="crp_title">Magento get CMS page content without header/footer</a></li></ul></div>'
categories:
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