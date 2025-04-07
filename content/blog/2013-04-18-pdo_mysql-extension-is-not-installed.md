---
id: 504
title: 'pdo_mysql extension is not installed'
date: '2013-04-18T20:11:15+00:00'
author: kalpesh
layout: post
tags:
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