---
id: 900
title: 'Magento: Sample local.xml template'
date: '2014-06-22T19:08:11+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - local.xml
---

Sample app/etc/local.xml file template. Change mysql database name, username and password with yours and clear the cache.

{{< highlight xml "style=emacs" >}}  
<config>  
 <global>  
 <install>  
 <date><![CDATA[Mon, 23 Sep 2013 19:53:16 +0000]]></date>  
 </install>  
 <crypt>  
 <key><![CDATA[414c9022922d31b62bbe4447356e4ed6]]></key>  
 </crypt>  
 <disable_local_modules>false</disable_local_modules>  
 <resources>  
 <db>  
 <table_prefix><![CDATA[]]></table_prefix> </db>  
 <default_setup>  
 <connection>  
 <host><![CDATA[127.0.0.1]]></host>  
 <username><![CDATA[MYSQL_USERNAME]]></username> <password><![CDATA[MYSQL_PASSWORD]]></password> <dbname><![CDATA[DATABASE_NAME]]></dbname>  
 <initstatements><![CDATA[SET NAMES utf8]]></initstatements>  
 <model><![CDATA[mysql4]]></model>  
 <type><![CDATA[pdo_mysql]]></type> <pdotype><![CDATA[]]></pdotype> <active>1</active>  
 </connection>  
 </default_setup>  
 </resources>  
 <session_save><![CDATA[files]]></session_save>  
 </global>  
 <admin>  
 <routers>  
 <adminhtml>  
 <args>  
 <frontname><![CDATA[admin]]></frontname>  
 </args>  
 </adminhtml>  
 </routers>  
 </admin>  
</config>{{< /highlight >}}