---
id: 760
title: 'Magento system config 404 error'
date: '2013-07-13T00:02:22+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=760'
permalink: /index.php/2013/07/13/magento-system-config-404-error/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-get-subcategories-of-a-category/"     class="crp_title">Magento get subcategories of a category by category ID</a></li></ul></div>'
categories:
    - Magento
    - 'Magento error'
tags:
    - admin
    - error
    - magento
---

Magento gives 404 error / Forbidden error / Access denied error when you try to open the screen of your newly written config/system XML code because either of 2 reasons.

1.) You have written the code CORRECTLY, but Magento needs to write permissions for that module in session to show it.  
– Just logout and login again and you should see your newly developed screen.

2.) You have some error in your ACL role code. Magento needs the ACL role information to allow admin view the admin module.  
– Check your ACL code definition again and make sure everything there is correct.

*Sample code of ACL to display custom menu item in navigation:*  
{{< highlight xml "style=emacs" >}}<config>  
 <acl>  
 <resources>  
 <all>  
 <title>Allow everything</title>  
 </all>  
 <admin>  
 <children>  
 <mycustommenu module="modulename" translate="title">  
 <title>Custom MENU</title>  
 <sort_order>500</sort_order>  
 <children>  
   
 <submenuitem module="modulename" translate="title">  
 <title>Custom SUB MENU</title>  
 <sort_order>10</sort_order>  
 </submenuitem>  
 </children>  
 </mycustommenu>  
 </children>  
 </admin>  
 </resources>  
 </acl>  
</config>{{< /highlight >}}  
  
*Sample code of ACL for new submenu under SYSTEM main menu in navigation:*  
{{< highlight xml "style=emacs" >}}<config>  
 <acl>  
 <resources>  
 <all>  
 <title>Allow everything</title>  
 </all>  
 <admin>  
 <children>  
 <system>  
 <children>  
 <mycustomsystem>  
 <title>SUB SYSTEM!</title>  
 </mycustomsystem>  
 </children>  
 </system>  
 </children>  
 </admin>  
 </resources>  
 </acl>  
</config>{{< /highlight >}}

*Sample code of ACL for new screen under System Configuration:*  
{{< highlight xml "style=emacs" >}}<config>  
 <acl>  
 <resources>  
 <all>  
 <title>Allow everything</title>  
 </all>  
 <admin>  
 <children>  
 <system>  
 <children>  
 <config>  
 <children>  
 <example translate="title">  
 <title>An Example Section</title>  
 <sort_order>100</sort_order>  
 </example>  
 </children>  
 </config>  
 </children>  
 </system>  
 </children>  
 </admin>  
 </resources>  
 </acl>  
</config>{{< /highlight >}}