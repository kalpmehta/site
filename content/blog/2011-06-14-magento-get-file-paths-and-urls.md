---
id: 79
title: 'Magento get file paths and URLs'
date: '2011-06-14T11:45:15+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=79'
permalink: /index.php/2011/06/14/magento-get-file-paths-and-urls/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-show-maintenance-mode-page-website-under-construction/"     class="crp_title">Magento: Show maintenance mode page (website under construction)</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li></ul></div>'
categories:
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