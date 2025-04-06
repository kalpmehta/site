---
id: 832
title: 'Magento debug XML (layout, config) files'
date: '2013-08-17T18:37:02+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=832'
permalink: /index.php/2013/08/17/magento-debug-xml-layout-config-files/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5774569437633998848&amp;type=U&amp;a=yyLm";s:5:"pDate";s:19:"2013-08-17 18:37:20";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"368803695669952513";s:5:"pDate";s:19:"2013-08-17 18:37:07";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/18/magento-client-denied-by-server-configuration/"     class="crp_title">Magento client denied by server configuration notice</a></li><li><a href="http://ka.lpe.sh/2013/07/13/magento-system-config-404-error/"     class="crp_title">Magento system config 404 error</a></li><li><a href="http://ka.lpe.sh/2012/07/26/php-xml-to-json-xml-to-array-json-to-array/"     class="crp_title">Convert PHP XML to JSON, XML to Array, JSON to Array</a></li><li><a href="http://ka.lpe.sh/2011/06/08/overriderewrite-magento-core-blocks-and-controllers/"     class="crp_title">Override/Rewrite Magento core blocks and controllers</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magentophp-convert-your-xml-object-to-array/"     class="crp_title">Magento/PHP: Convert your XML Object to Array</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - debug
    - magento
    - xml
---

In Magento if there is any error in XML file, Magento silently ignores it and continues further parsing. So you never get to know where is the actual error and makes it difficult to debug. You can’t even do any logging in XML file and also Magento don’t tell that error is in XML. It makes debugging almost impossible and ends up wasting in hours to find some silly mistake.

But we can know if there is any error in XML (layout.xml or config.xml or any xml file) if you use below code in the controller action which is being called. The browser will display WHOLE XML code and if it encounters any error in it, simply gives where is the error in the XML tree.

If you are trying to load let’s say Product View page, then put this code in Mage/Catalog/controllers/ProductController.php file’s viewAction() method temporarily to display whole XML tree to find out error(s) if any. As we are saying to display the page as XML, the page will break if it finds any mal-formed XML code and will show where is the mistake.

{{< highlight php "style=emacs" >}}header(“Content-Type: text/xml”);  
echo Mage::app()->getConfig()->getNode()->asXml();exit;{{< /highlight >}}

If you want to debug Layout Handles only, you can just check by this code:  
{{< highlight php "style=emacs" >}}header(“Content-Type: text/xml”);  
echo Mage::app()->getLayout()->getUpdate()->getHandles();exit;{{< /highlight >}}