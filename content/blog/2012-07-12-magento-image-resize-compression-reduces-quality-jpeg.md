---
id: 266
title: 'Magento: Image resize/compression reduces quality of JPEG'
date: '2012-07-12T13:56:20+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'gd2 compression'
    - 'image resize blur'
    - 'magento bad quality image'
    - 'magento image distorts'
    - 'magento jpeg poor quality'
---

In Magento, image quality is distorted when it’s resized in Category page as well as Product page. This is very bad if you are running an eCommerce website because image is the only thing which gives best impression to your customers. There are several complains regarding this in Magento forums with different answers. Some even suggest to use ImageMagick over the default Gd2 library.

If you don’t want to switch to ImageMagick and also don’t want to do much changes, here is a simple solution.

1.) Copy app/code/core/Mage/Catalog/Helper/Image.php  
2.) Paste it in local (app/code/local/ , create directories Mage/Catalog/Helper if it’s not there)  
 So the final structure will be app/code/local/Mage/Catalog/Helper/Image.php  
3.) Edit newly pasted Image.php’s init() method, just after it sets “watermark size”, add a line:  
 {{< highlight php "style=emacs" >}}$this->setQuality(100);{{< /highlight >}}  
4.) Save, flush image cache, run any category or product page and see the difference!

Hope this helps!