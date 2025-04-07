---
id: 281
title: 'Migrate magento to new server / domain / database / host'
date: '2012-07-21T19:24:19+00:00'
author: kalpesh
layout: post
tags:
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