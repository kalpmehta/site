---
id: 319
title: 'Magento: How to delete/remove all products from all categories'
date: '2012-08-09T13:20:06+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'delete all products'
    - 'magento empty all product tables'
    - 'magento remove products'
    - 'remove products from categories'
---

When you are using some script to automatically add products to categories from XLS file to your Magento system, you may need to delete all products frequently for testing purpose. It’s not as easy to mark all products and press delete button in admin. No, it’s not like that, you need to delete all products, remove them from their linked categories, reset the inventory, etc. so many things to do.

Below is the MySQL queries that will make your task easier. By running all the queries, it will delete all the products in your Magento system. Use it carefully, it’s going to delete everything without an option to rollback.

{{< highlight php "style=emacs" >}}SET FOREIGN_KEY_CHECKS = 0;  
TRUNCATE TABLE `catalog_product_bundle_option`;  
TRUNCATE TABLE `catalog_product_bundle_option_value`;  
TRUNCATE TABLE `catalog_product_bundle_selection`;  
TRUNCATE TABLE `catalog_product_entity_datetime`;  
TRUNCATE TABLE `catalog_product_entity_decimal`;  
TRUNCATE TABLE `catalog_product_entity_gallery`;  
TRUNCATE TABLE `catalog_product_entity_int`;  
TRUNCATE TABLE `catalog_product_entity_media_gallery`;  
TRUNCATE TABLE `catalog_product_entity_media_gallery_value`;  
TRUNCATE TABLE `catalog_product_entity_text`;  
TRUNCATE TABLE `catalog_product_entity_tier_price`;  
TRUNCATE TABLE `catalog_product_entity_varchar`;  
TRUNCATE TABLE `catalog_product_link`;  
TRUNCATE TABLE `catalog_product_link_attribute`;  
TRUNCATE TABLE `catalog_product_link_attribute_decimal`;  
TRUNCATE TABLE `catalog_product_link_attribute_int`;  
TRUNCATE TABLE `catalog_product_link_attribute_varchar`;  
TRUNCATE TABLE `catalog_product_link_type`;  
TRUNCATE TABLE `catalog_product_option`;  
TRUNCATE TABLE `catalog_product_option_price`;  
TRUNCATE TABLE `catalog_product_option_title`;  
TRUNCATE TABLE `catalog_product_option_type_price`;  
TRUNCATE TABLE `catalog_product_option_type_title`;  
TRUNCATE TABLE `catalog_product_option_type_value`;  
TRUNCATE TABLE `catalog_product_super_attribute`;  
TRUNCATE TABLE `catalog_product_super_attribute_label`;  
TRUNCATE TABLE `catalog_product_super_attribute_pricing`;  
TRUNCATE TABLE `catalog_product_super_link`;  
TRUNCATE TABLE `catalog_product_enabled_index`;  
TRUNCATE TABLE `catalog_product_website`;  
TRUNCATE TABLE `catalog_product_entity`;  
TRUNCATE TABLE `cataloginventory_stock`;  
TRUNCATE TABLE `cataloginventory_stock_item`;  
TRUNCATE TABLE `cataloginventory_stock_status`;  
TRUNCATE TABLE `catalog_product_link`;  
TRUNCATE TABLE `catalog_product_link_type`;  
TRUNCATE TABLE `catalog_product_option`;  
TRUNCATE TABLE `catalog_product_option_type_value`;  
TRUNCATE TABLE `catalog_product_super_attribute`;  
TRUNCATE TABLE `catalog_product_entity`;  
TRUNCATE TABLE `cataloginventory_stock`;  
DELETE FROM catalog_product_flat_1;  
DELETE FROM catalog_product_flat_10;  
DELETE FROM catalog_product_flat_11;  
DELETE FROM catalog_product_flat_12;  
DELETE FROM catalog_product_flat_13;  
DELETE FROM catalog_product_flat_14;  
DELETE FROM catalog_product_flat_15;  
DELETE FROM catalog_product_flat_16;  
DELETE FROM catalog_product_flat_17;  
DELETE FROM catalog_product_flat_18;  
DELETE FROM catalog_product_flat_19;  
DELETE FROM catalog_product_flat_2;  
DELETE FROM catalog_product_flat_20;  
DELETE FROM catalog_product_flat_21;  
DELETE FROM catalog_product_flat_22;  
DELETE FROM catalog_product_flat_23;  
DELETE FROM catalog_product_flat_24;  
DELETE FROM catalog_product_flat_25;  
DELETE FROM catalog_product_flat_26;  
DELETE FROM catalog_product_flat_27;  
DELETE FROM catalog_product_flat_28;  
DELETE FROM catalog_product_flat_29;  
DELETE FROM catalog_product_flat_3;  
DELETE FROM catalog_product_flat_30;  
DELETE FROM catalog_product_flat_31;  
DELETE FROM catalog_product_flat_32;  
DELETE FROM catalog_product_flat_33;  
DELETE FROM catalog_product_flat_34;  
DELETE FROM catalog_product_flat_35;  
DELETE FROM catalog_product_flat_36;  
DELETE FROM catalog_product_flat_37;  
DELETE FROM catalog_product_flat_4;  
DELETE FROM catalog_product_flat_5;  
DELETE FROM catalog_product_flat_6;  
DELETE FROM catalog_product_flat_7;  
DELETE FROM catalog_product_flat_8;  
DELETE FROM catalog_product_flat_9;  
SET FOREIGN_KEY_CHECKS = 1;

insert into `catalog_product_link_type`(`link_type_id`,`code`) values (1,’relation’),(2,’bundle’),(3,’super’),(4,’up_sell’),(5,’cross_sell’);  
insert into `catalog_product_link_attribute`(`product_link_attribute_id`,`link_type_id`,`product_link_attribute_code`,`data_type`) values (1,2,’qty’,’decimal’),(2,1,’position’,’int’),(3,4,’position’,’int’),(4,5,’position’,’int’),(6,1,’qty’,’decimal’),(7,3,’position’,’int’),(8,3,’qty’,’decimal’);  
insert into `cataloginventory_stock`(`stock_id`,`stock_name`) values (1,’Default’);{{< /highlight >}}

Now go to System > Index Management, and re-index all indexes.

Hope this helps!