---
id: 900
title: 'Magento: Sample local.xml template'
date: '2014-06-22T19:08:11+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=900'
permalink: /index.php/2014/06/22/magento-sample-local-xml-template/
snapEdIT:
    - '1'
snapFB:
    - 's:193:"a:1:{i:0;a:5:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
snapTW:
    - 's:126:"a:1:{i:0;a:4:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2013/06/20/how-to-install-orocrm/"     class="crp_title">OroCRM Installation guide</a></li><li><a href="http://ka.lpe.sh/2013/12/01/magento-redis-read-error-on-connection/"     class="crp_title">Magento Redis read error on connection</a></li></ul></div>'
categories:
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