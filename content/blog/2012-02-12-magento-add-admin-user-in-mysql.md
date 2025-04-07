---
id: 214
title: 'Magento add admin user in MySQL'
date: '2012-02-12T11:26:35+00:00'
author: kalpesh
layout: post
tags:
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