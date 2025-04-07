---
id: 79
title: 'Magento get file paths and URLs'
date: '2011-06-14T11:45:15+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'absolute path'
    - directory
    - magento
    - 'relative path'
    - url
---

Get URL paths of your magento folder structure – Absolute URL Path

**Mage::getBaseUrl()** => Gets base url path e.g. http://my.website.com/

**Mage::getBaseUrl(‘media’**) => Gets MEDIA folder path e.g. http://my.website.com/media/

**Mage::getBaseUrl(‘js’)** => Gets JS folder path e.g. http://my.website.com/js/

**Mage::getBaseUrl(‘skin’)** => Gets SKIN folder path e.g. http://my.website.com/skin/

Get DIRECTORY paths (physical location of your folders on the server) – Relative URL Path

**Mage::getBaseDir()** => Gives you your Magento installation folder / root folder e.g. /home/kalpesh/workspace/magento

**Mage::getBaseDir(‘app’)** => Gives you your Magento’s APP directory file location e.g. /home/kalpesh/workspace/magento/app

**Mage::getBaseDir(‘design’)** => Gives you your Magento’s DESIGN directory file location e.g. /home/kalpesh/workspace/magento/design

**Mage::getBaseDir(‘media’)** => Gives MEDIA directory file path

**Mage::getBaseDir(‘code’)** => Gives CODE directory file path

**Mage::getBaseDir(‘lib’)** => Gives LIB directory file path

Get Current URL – whole URL path

**Mage::helper(‘core/url’)->getCurrentUrl()**