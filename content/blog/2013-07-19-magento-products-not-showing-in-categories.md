---
id: 780
title: 'Magento products not showing in categories'
date: '2013-07-19T14:19:50+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=780'
permalink: /index.php/2013/07/19/magento-products-not-showing-in-categories/
snapEdIT:
    - '1'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li><li><a href="http://ka.lpe.sh/2013/07/16/magento-get-products-without-category/"     class="crp_title">Magento get products without category</a></li><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/05/20/magento-pinterest-extension-plugin-autopin-multiple-product-images/"     class="crp_title">Magento Pinterest extension Auto Pin multiple product images Plugin</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-filter-products-by-status/"     class="crp_title">Magento filter products by status</a></li></ul></div>'
snap_isAutoPosted:
    - '1'
snapFB:
    - 's:297:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200405899454329";s:5:"pDate";s:19:"2013-07-19 14:20:00";}}";'
snapLI:
    - 's:405:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5763995432439017472&amp;type=U&amp;a=SzEx";s:5:"pDate";s:19:"2013-07-19 14:20:01";}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"358229831592329216";s:5:"pDate";s:19:"2013-07-19 14:20:22";}}";'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento error'
    - 'Magento frontend'
tags:
    - category
    - error
    - magento
    - product
---

If your Magento products are not showing up in frontend category pages, that can be because one or more of the below points are not done correctly.

The products must have following set correctly to appear in the category pages in frontend. You can check all the below things in Manage Products screen of any individual product.  
– *Status* must be Enabled (under General tab)  
– *Visiblility* should be Catalog OR Catalog, Search (under General tab)  
– Stock *Qty* (quantity) should be greater than *Qty for Item’s Status to Become Out of Stock* (under Inventory tab)  
– *Stock Availability* must be IN STOCK  
– *Category* should be assigned (under Categories tab)  
– *Website* must be assigned (under Websites tab)

Clear the cache, re-index the indexes related to product (Product prices, Product flat data and Category products) and everything should work as expected.

This post is written to address the following issue:  
magento products not displaying in categories  
magento products not showing in categories  
magento items not showing in categories  
magento products not showing up in categories  
magento products not showing under categories  
magento products not displaying on category page  
magento product images not showing in category  
magento configurable product not showing in category  
magento new product not showing in category

If you are unable to see Product Images in frontend category pages, check this blog post to resolve it: [http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/](http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/ "Magento cannot see product images in category page")