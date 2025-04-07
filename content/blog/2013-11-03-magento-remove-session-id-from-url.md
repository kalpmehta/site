---
id: 847
title: 'Magento remove session id from URL'
date: '2013-11-03T20:00:28+00:00'
author: kalpesh
layout: post
tags:
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