---
id: 117
title: 'Upgrading Android 2.2 (Froyo) to Gingerbread (2.3.4) &#8211; Samsung Galaxy Fit S5670'
date: '2011-09-18T18:38:07+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=117'
permalink: /index.php/2011/09/18/upgrading-android-2-2-froyo-to-gingerbread-2-3-4-samsung-galaxy-fit-s5670/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li><li><a href="http://ka.lpe.sh/2012/11/02/buy-pinterest-autopost-images-right-from-your-website/"     class="crp_title">Buy: Pinterest AutoPost images right from your website!</a></li><li><a href="http://ka.lpe.sh/2011/07/10/magento-show-only-specific-attributes-in-layered-navigation/"     class="crp_title">Magento: Show only specific attributes in layered navigation</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li></ul></div>'
categories:
    - Mobile
tags:
    - android
    - froyo
    - gingerbread
    - Samsung
    - upgrade
---

If you have purchased Samsung galaxy fit S5670 mobile phone, you must have noticed that it has very short battery life. Also you may have experienced sudden switch off of your mobile and weird behavior. This is due to some bugs in Android OS version 2.2 (froyo).

To fix this, you will have to upgrade your android OS from 2.2 to 2.3.4 version which will increase your battery life to some extent. Before proceeding backup all your important data (contacts, messages, etc..) so that if something goes wrong in between, you are on your safer side. So here are the steps to follow:

1\. Download [ODIN Multi-downloader v4.38](http://www.4shared.com/file/mjuSJQDG/odin_multi_downloader_v438.html) – 444 KB  
2\. Download [Gingerbread Firmware](http://hotfile.com/dl/120514743/bf7c5b1/S5670XXKPI.rar.html) – 113 MB  
3\. Turn off you samsung mobile phone   
4\. Extract S5670XXKPI and run ODIN on your PC  
5\. Select OPS file: BENI_v1.0.ops (from the extracted folder S5670XXKPI)  
 – Click BOOT button and select: APBOOT_S5670xxxxx_CL913243_REV01_user_low_true.tar.md5  
 – Click Phone button and select: MODEM_S5670xxxxx_CL913243_REV01.tar.md5  
 – Click PDA button and select: CODE_S5670xxxxx_CL913243_REV01_user_low_true.tar.md5  
 – Click CSC button and select: CSC_S5670xxxxxx_CL913243_REV01_user_low_true.tar.md5  
6\. Turn your phone off. Switch it ON in downloading mode by pressing MIDDLE KEY + VOLUME DOWN + POWER buttons  
7\. Connect USB cable and check ODIN should read the COM port number. You will see yellow color box.  
8\. Now click Start. Upgrade begins. Don’t interrupt anything until you see PASS in your ODIN software.

Once you are done with the upgrade process, your mobile will start in some different language (Russian). To change the language to English (US) click on Menu -> Settings Icon -> A icon -> Click First option -> Scroll down to English (US).

Hope it helps!