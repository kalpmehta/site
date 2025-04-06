---
id: 500
title: 'Magento client denied by server configuration notice'
date: '2013-04-18T20:00:20+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=500'
permalink: /index.php/2013/04/18/magento-client-denied-by-server-configuration/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2012/07/12/magento-image-resize-compression-reduces-quality-jpeg/"     class="crp_title">Magento: Image resize/compression reduces quality of JPEG</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento error'
tags:
    - 'client denied by server configuration'
    - 'magento error'
---

Magento client denied by server configuration: /var/www/magento/app/etc/local.xml .. This is not the error, but just a message type thing displayed in apache error log and firebug console. Nothing to worry here, it’s just a security check from web server and you should ignore it.

If you don’t like it then you can turn it off by writing few lines of code in app/design/adminhtml/default/default/layout/local.xml  
{{< highlight xml "style=emacs" >}}<layout>  
 <default>  
 <remove name="notification_security"></remove>  
 <remove name="notification_survey"></remove>  
 </default>  
</layout>{{< /highlight >}}

Clear cache as usual, and you should get rid of this message.