---
id: 995
title: 'Magento 2 Security Bug in Customer Address section (Resolved)'
date: '2015-03-28T06:31:02+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=995'
permalink: /index.php/2015/03/28/magento-2-security-bug/
crp_related_posts_feed:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2015/03/20/magento-incorrect-sales-order-report-dst/"     class="crp_title">Magento bug: Incorrect sales order report during DST</a></li><li><a href="http://ka.lpe.sh/2014/11/07/magento-real-ip-address-behind-proxy/"     class="crp_title">Magento: Get real IP address behind a proxy</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2015/03/28/magento-checkout-cart-500-error/"     class="crp_title">Magento bug &#8211; Checkout cart 500 error &#8211; Redirect loops</a></li><li><a href="http://ka.lpe.sh/2015/03/28/magento-ee-1-14-broken-category-product-sitemap-urls/"     class="crp_title">Magento EE 1.14 &#8211; Broken category &#038; product sitemap URLs</a></li></ul><div class="crp_clear"></div></div>'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2015/03/20/magento-incorrect-sales-order-report-dst/"     class="crp_title">Magento bug: Incorrect sales order report during DST</a></li><li><a href="http://ka.lpe.sh/2014/11/07/magento-real-ip-address-behind-proxy/"     class="crp_title">Magento: Get real IP address behind a proxy</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2013/06/10/orocrm/"     class="crp_title">OroCRM</a></li><li><a href="http://ka.lpe.sh/2015/03/28/magento-ee-1-14-broken-category-product-sitemap-urls/"     class="crp_title">Magento EE 1.14 &#8211; Broken category &#038; product sitemap URLs</a></li></ul></div>'
categories:
    - Magento2
tags:
    - bug
    - magento2
    - security
---

Magento 2 had a serious security bug where a website user can view and edit any customer’s address very easily. I reported this issue to Magento 2 team and they quickly fixed it and rolled it out in new beta version. All the beta versions up to **0.42.0-beta11** were affected, and from **0.74.0-beta1** it is fixed (I have not tested it yet).

Details about the bug and progress: <https://github.com/magento/magento2/issues/1107>

If you are using the affected Magento 2 versions for online demo or development please upgrade it. Though people use fake address in Demo stores, it is likely that some of them could have used their real address and details which can be accessible by anyone who knows about this bug.