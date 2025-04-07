---
id: 832
title: 'Magento debug XML (layout, config) files'
date: '2013-08-17T18:37:02+00:00'
author: kalpesh
layout: post
tags:
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