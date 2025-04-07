---
id: 500
title: 'Magento client denied by server configuration notice'
date: '2013-04-18T20:00:20+00:00'
author: kalpesh
layout: post
tags:
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