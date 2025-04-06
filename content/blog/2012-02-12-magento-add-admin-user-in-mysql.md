---
id: 214
title: 'Magento add admin user in MySQL'
date: '2012-02-12T11:26:35+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=214'
permalink: /index.php/2012/02/12/magento-add-admin-user-in-mysql/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-mysql-records-null-values-not-getting-fetched/"     class="crp_title">Magento: Mysql records with NULL values are not fetched in query</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-customer-details-customer-id-name-email/"     class="crp_title">Magento: Get customer details : customer id, name, email</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - MySQL
tags:
    - 'admin user'
    - magento
    - mysql
---

In Magento, if you want to create a new user directly in Mysql, it’s not that easy to insert one record in admin_user table.  
You need to also update the privileges and inserting new admin’s roles.  
So here is a Mysql script which will create a new admin user with all privileges.

Replace FIRSTNAME, LASTNAME, EMAIL, USERNAME, PASSWORD with your desired values.  
{{< highlight http >}}   
insert into admin_user  
select  
(select max(user_id) + 1 from admin_user) user_id,  
‘FIRSTNAME’ first_name,  
‘LASTNAME’ last_name,  
‘TEST@EMAIL.COM’ email,  
‘USERNAME’ username,  
MD5(‘PASSWORD’) password,  
now() created,  
NULL modified,  
NULL logdate,  
0 lognum,  
0 reload_acl_flag,  
1 is_active,  
(select max(extra) from admin_user where extra is not null) extra,  
NULL,  
NULL;

insert into admin_role  
select  
(select max(role_id) + 1 from admin_role) role_id,  
(select role_id from admin_role where role_name = ‘Administrators’) parent_id,  
2 tree_level,  
0 sort_order,  
‘U’ role_type,  
(select user_id from admin_user where username = ‘USERNAME’) user_id,  
‘USERNAME’ role_name  
{{< /highlight >}}