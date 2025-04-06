---
id: 281
title: 'Migrate magento to new server / domain / database / host'
date: '2012-07-21T19:24:19+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=281'
permalink: /index.php/2012/07/21/migrate-magento-to-new-server-domain-database-host/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2013/02/02/magento-create-database-backups-daily-programatically-by-cron/"     class="crp_title">Magento: Create database backups daily programatically by cron</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - database
    - domain
    - host
    - magento
    - migrate
    - move
    - new
    - server
---

Move or migrate magento to new server, domain, database, host, anything by following the steps below.

To configure your Magento with a new domain, you will need to do following steps:

– Copy whole Magento project from current server and paste it to the new server.  
You can do server-to-server transfer. First, tar.gz your magento project  
`tar -cvf magento.tar.gz magento`  
Then copy it to your new server from old server  
`scp magento.tar.gz root@your.ip.address.here:/var/www/.`

– Backup the database (Admin -> System -> Tools -> Backup)  
You can also take backup through phpMyAdmin, or by mysql.  
`mysqldump -u user -p database > /path/to/keep/db.sql`

– Logout from your old server. Login to new server.  
Extract the file magento.tar.gz that you sent from old server  
`tar -zxvf magento.tar.gz`  
  
– Delete all directory or files that are there in cache folder  
`rm -rf var/cache/*`

– Edit local.xml that is in magento/app/etc/local.xml and change mysql username, password, database as per new server credentials

– Import the backed up database. Before that create empty database to dump tables in it.  
`mysql -u root -p 'password';<br></br>create database dbname;<br></br>exit;<br></br>mysql -u root -p -d dbname < /path/to/your/db.sql`

\- Edit the database to change it to your new domain name. Search in core_config_data table for old domain.  
`select * from core_config_data where path like '%secure/base_url';`  
and update it with your new domain  
`update core_config_data set value='http://mysite.com/' where path like '%secure/base_url';`