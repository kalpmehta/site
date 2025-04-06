---
id: 504
title: 'pdo_mysql extension is not installed'
date: '2013-04-18T20:11:15+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=504'
permalink: /index.php/2013/04/18/pdo_mysql-extension-is-not-installed/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2012/08/03/mysql-find-column-name-in-any-tables-having-it-in-whole-database/"     class="crp_title">Mysql: Find column name in any table(s) having it in whole database</a></li><li><a href="http://ka.lpe.sh/2012/10/10/ubuntu-delete-temporary-cache-files/"     class="crp_title">Ubuntu: Delete temporary/cache files</a></li></ul></div>'
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
categories:
    - Linux
    - Magento
    - 'Magento error'
    - MySQL
tags:
    - extension
    - 'not installed'
    - pdo_mysql
---

PHP Mysql Error: pdo_mysql extension is not installed.

Magento needs PDO Mysql extension for database connection and related things, so if you don’t have pdo_mysql extension enabled Magento will complain about this and will not proceed further installation. If you are not sure what PDO is, it’s high time for you to look at <http://php.net/manual/en/ref.pdo-mysql.php>

Coming back to error, to resolve this you will need to edit your php.ini file where it says:  
;extension=pdo_mysql.so

Just uncomment the line by removing front semincolon, so it becomes  
extension=pdo_mysql.so

Save it and restart the server, the error should go.

If you are on Windows, then that line should read:

extension=php_pdo_mysql.dll

If you don’t find pdo_mysql in php.ini, **install** php5-mysql by running the command:

sudo apt-get install php5-mysql (on Ubuntu)

sudo yum install php-mysql (on Redhat, Fedora, CentOS)