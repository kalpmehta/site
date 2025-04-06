---
id: 433
title: 'Mysql root password reset or create'
date: '2013-01-08T15:13:10+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=433'
permalink: /index.php/2013/01/08/mysql-root-password-reset/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/12/magento-add-admin-user-in-mysql/"     class="crp_title">Magento add admin user in MySQL</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-show-maintenance-mode-page-website-under-construction/"     class="crp_title">Magento: Show maintenance mode page (website under construction)</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-register-guest-user-to-website-if-email-provided/"     class="crp_title">Magento: Register guest user to website if email provided</a></li></ul></div>'
categories:
    - Linux
    - MySQL
tags:
    - create
    - mysql
    - reset
    - 'root password'
---

Mysql root password reset easily by following below instructions. For those who want to create (if no root user in mysql) or reset the password for the Root user in Mysql (in Linux), this post is definately going to help you. I had a tough time in getting this to work, so thought to share it with anyone facing the same problem.

You need to use **–skip-grant-tables** if you don’t know mysql password to login. You can use it like this:

*/usr/bin/mysqld_safe –skip-grant-tables &amp;*

Once you run the above command on terminal, write *mysql* and hit enter. That’s because you already said Mysql that you want to skip all the privileges checking and allowing you with all the database access without password.

You should be inside mysql now. Now execute the command *use mysql;* because we are going to create/change the user in “mysql” database.  
  
Now, check if you have the root user in the “user” table. Do this by:  
*select * from user;*

If you already have root user, just execute this to change the password:  
*UPDATE user SET Password=PASSWORD(‘new-password’) WHERE User=’root’;*

If you don’t have any records in user table, create one:  
*insert into `user` (`Host`, `User`, `Password`, `Select_priv`, `Insert_priv`, `Update_priv`, `Delete_priv`, `Create_priv`, `Drop_priv`, `Reload_priv`, `Shutdown_priv`, `Process_priv`, `File_priv`, `Grant_priv`, `References_priv`, `Index_priv`, `Alter_priv`, `Show_db_priv`, `Super_priv`, `Create_tmp_table_priv`, `Lock_tables_priv`, `Execute_priv`, `Repl_slave_priv`, `Repl_client_priv`, `Create_view_priv`, `Show_view_priv`, `Create_routine_priv`, `Alter_routine_priv`, `Create_user_priv`, `ssl_type`, `ssl_cipher`, `x509_issuer`, `x509_subject`, `max_questions`, `max_updates`, `max_connections`, `max_user_connections`)  
values(‘localhost’,’root’,”,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’, ‘Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,’Y’,”,”,”,”,’0′,’0′,’0′,’0′);*

This creates new user “root” with no password.  
To set a password, use the above UPDATE command.

After it’s done, don’t forget to execute *flush privileges;*

Restart mysql and you should be now able to login with root user and your new password.