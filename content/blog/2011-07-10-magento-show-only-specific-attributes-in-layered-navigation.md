---
id: 107
title: 'Magento: Show only specific attributes in layered navigation'
date: '2011-07-10T06:02:34+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=107'
permalink: /index.php/2011/07/10/magento-show-only-specific-attributes-in-layered-navigation/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2013/02/07/magento-add-product-custom-attribute-options-dynamically/"     class="crp_title">Magento: Add product custom attribute options dynamically</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - admin
    - magento
    - navigation
---

In Magento, if you have lots of attributes (e.g. Type, Size, Price, Color, etc.) defined for categories, all are shown in the layered navigation on the left side. This may be sometimes annoying as they may break the website design. It is possible to disable the desired attributes from displaying on frontend.

The solution is, go to:

– Magento Backend -> Catalog Tab -> Attributes -> Manage Attributes  
– Click the attributes you do not want to display in layered navigation  
– Select NO where it says “Use in Layered Navigation”  
– Save

Now all the attributes with Use in Layered Navation as Yes will only show in frontend Shopping options.