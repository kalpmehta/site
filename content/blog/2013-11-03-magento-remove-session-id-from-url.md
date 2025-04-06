---
id: 847
title: 'Magento remove session id from URL'
date: '2013-11-03T20:00:28+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=847'
permalink: /index.php/2013/11/03/magento-remove-session-id-from-url/
snapEdIT:
    - '1'
snapFB:
    - 's:193:"a:1:{i:0;a:5:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";}}";'
snapLI:
    - 's:205:"a:1:{i:0;a:5:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
    - '1'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"397090974050287616";s:5:"pDate";s:19:"2013-11-03 20:00:40";}}";'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/06/19/magento-get-and-set-variables-in-session/"     class="crp_title">Magento: Get and set variables in session</a></li><li><a href="http://ka.lpe.sh/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/"     class="crp_title">Magento 1.5: Cannot login to admin panel after fresh install</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-current-url/"     class="crp_title">Magento get current url with and without parameters</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - magento
    - session
    - url
---

Magento displays session ID in url, something like:  
{{< highlight http >}} http://loca.lho.st?__SID=2wewesfdgfsdm{{< /highlight >}}

You can remove this in two ways:

1\. Go to your **Magento admin panel > System > Configuration > Web**.  
Under Session Validation Settings, set “No” against label “Use SID on the Frontend”.  
If this doesn’t work, then move to option two below.

2\. Edit the file at **app/code/core/Mage/Core/Model/App.php** (somewhere around line 222),  
{{< highlight php "style=emacs" >}}protected $_useSessionInUrl = true;{{< /highlight >}}  
Change that value to “false”. That should now prevent session IDs appearing in URL.