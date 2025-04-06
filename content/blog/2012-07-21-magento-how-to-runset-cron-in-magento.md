---
id: 285
title: 'Magento: How to run/set cron in Magento'
date: '2012-07-21T19:57:34+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=285'
permalink: /index.php/2012/07/21/magento-how-to-runset-cron-in-magento/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'magento cron'
    - 'set run cron in magento'
---

Ever came with the requirement where you need to set cron for periodically running certain jobs automatically? If you are new to cron in Magento, this blog post is going to help you out. Cron is a time-based job scheduler in Unix-like computer operating systems.

There are basically two crons: one is **system’s cron** (Unix, where it will trigger the specified file, for each specified time (in terms of minute, hour, day, week, year) AND another is **Magento’s internal cron** where it will decide which file and method to call to complete the operation.  
  
– First, you need to add following snipped in your module’s config.xml file, inside <config> node:</config>

{{< highlight xml "style=emacs" >}}<crontab>  
 <jobs>  
 <cron_name_must_be_unique>  
 <schedule>  
   
 <cron_expr>0 0 * * *</cron_expr>  
 </schedule>  
 <run>  
   
 <model>modulename/modelname::methodname</model>  
 </run>  
 </cron_name_must_be_unique>  
 </jobs>  
</crontab>{{< /highlight >}}

– Now open crontab of your system, by typing this in terminal:  
`crontab -l`  
This will list the cron defined in system, check if there is already cron set up for Magento, you don’t need to do anything here.  
Else, type this in terminal:  
`crontab -e`  
and add the below line at the end of file:  
`*/5 * * * * /bin/sh /var/www/magento/cron.sh`  
(this will run system’s cron every 5 minutes, you can change it as per your need)