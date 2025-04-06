---
id: 630
title: 'Magento Recoverable Error Argument 1 passed to Mage _Core _Model _Store ::setWebsite() must be an instance of Mage_Core_Model_Website'
date: '2013-05-22T17:37:10+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=630'
permalink: /index.php/2013/05/22/magento-recoverable-error-argument-1-passed-to/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento error'
tags:
    - admin
    - error
    - magento
---

Magento Recoverable Error: Argument 1 passed to Mage_Core_Model_Store::setWebsite() must be an instance of Mage_Core_Model_Website, null given, called in /var/www/xxx/app/code/core/Mage/Core/Model/App.php on line 634 and defined in /var/www/xxx/app/code/core/Mage/Core/Model/Store.php on line 395

When migrating Magento site from old server to new server, this error often occurs and appears in var/log/system.log. It prevents your Magento Admin to load JS and CSS files hence your admin panel becomes skinless.

The solution to get rid of this and load JS and CSS files is to run the following mysql commands in Mysql console or phpMyAdmin.

{{< highlight mariadb "style=emacs" >}}SET FOREIGN_KEY_CHECKS=0;  
UPDATE `core_store` SET store_id = 0 WHERE code=’admin’;  
UPDATE `core_store_group` SET group_id = 0 WHERE name=’Default’;  
UPDATE `core_website` SET website_id = 0 WHERE code=’admin’;  
UPDATE `customer_group` SET customer_group_id = 0 WHERE customer_group_code=’NOT LOGGED IN’;  
SET FOREIGN_KEY_CHECKS=1;{{< /highlight >}}

What the above mysql commands does is:  
– Disables foreign key checks on tables so that you don’t get any foreign key errors while executing immediate update queries.  
– Updates store, store_group and website tables with ID = 0, for admin user

Once the above set of queries are executed, don’t forget to **clear cache** to reflect your changes.