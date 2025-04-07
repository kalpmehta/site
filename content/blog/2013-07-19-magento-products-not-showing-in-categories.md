---
id: 780
title: 'Magento products not showing in categories'
date: '2013-07-19T14:19:50+00:00'
author: kalpesh
layout: post
tags:
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