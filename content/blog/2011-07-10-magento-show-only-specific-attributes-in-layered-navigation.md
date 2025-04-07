---
id: 107
title: 'Magento: Show only specific attributes in layered navigation'
date: '2011-07-10T06:02:34+00:00'
author: kalpesh
layout: post
tags:
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