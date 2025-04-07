---
id: 166
title: 'Magento: Show maintenance mode page (website under construction)'
date: '2011-12-31T17:49:50+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - magento
    - 'maintenance mode'
    - 'site under construction'
---

If you want your Magento website to show in maintenance mode, you will have to do two things.

1\. Create a file name **maintenance.flag** in your magento root directory. Contents under this file doesn’t matter, you can keep it empty.  
2\. Change the maintenance file (located in **magento root -> errors -> default** directory) to show proper message when user visits your website.