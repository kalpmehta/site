---
id: 335
title: 'Ubuntu: Delete temporary/cache files'
date: '2012-10-10T21:13:27+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=335'
permalink: /index.php/2012/10/10/ubuntu-delete-temporary-cache-files/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/04/18/pdo_mysql-extension-is-not-installed/"     class="crp_title">pdo_mysql extension is not installed</a></li><li><a href="http://ka.lpe.sh/2012/08/09/magento-how-to-delete-remove-all-products-from-all-categories/"     class="crp_title">Magento: How to delete/remove all products from all categories</a></li><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li></ul></div>'
categories:
    - Linux
tags:
    - 'clean ubuntu'
    - 'delete cache files'
    - 'ubuntu remove temporary files'
---

It’s necessary to clean unnecessary files from your operating system and free up space. In Ubuntu, this is very easy if you have admin privileges.

Below command will remove all the unnecessary package files, which are no longer used by their packages. You can say they are orphaned files, not needed anymore.  
**sudo apt-get autoremove**

Below command will remove all the cache and unnecessary files from your system. It will delete everything and make your system clean from temporary files and orphaned files.  
**sudo apt-get clean**