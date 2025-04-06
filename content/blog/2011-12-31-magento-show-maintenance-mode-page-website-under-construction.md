---
id: 166
title: 'Magento: Show maintenance mode page (website under construction)'
date: '2011-12-31T17:49:50+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=166'
permalink: /index.php/2011/12/31/magento-show-maintenance-mode-page-website-under-construction/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2012/01/29/magento-advanced-interview-questions/"     class="crp_title">Magento Advanced Interview Questions</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li></ul></div>'
categories:
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