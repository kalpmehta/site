---
id: 672
title: 'jQuery redirect page, with javascript alternative'
date: '2013-05-29T11:31:29+00:00'
author: kalpesh
layout: post
tags:
    - jQuery
tags:
    - jquery
    - redirect
---

![jQuery javascript framework](http://ka.lpe.sh/uploads/2013/06/jquery-logo.png)jQuery redirect one page to another using the following code:  
{{< highlight js "style=emacs" >}}var your_url = ‘http://ka.lpe.sh/’; //change this to your url  
$(location).attr(‘href’,’your_url’);{{< /highlight >}}

Above code works to redirect page in jQuery, but javascript code is good alternative here.

Using javascript to redirect your page using below code, which is better than jQuery, will do the job:  
{{< highlight js "style=emacs" >}}window.location.replace(“http://ka.lpe.sh/”);{{< /highlight >}}

Another javascript approach which will mock as if the URL is being clicked to redirect is:  
{{< highlight js "style=emacs" >}}window.location.href = “http://ka.lpe.sh/”;{{< /highlight >}}

Even this will do the trick in javascript, which sets your URL in a window object and assigns it to anchor tag’s href attribute automatically:  
{{< highlight js "style=emacs" >}}window.location = “http://ka.lpe.sh/”;{{< /highlight >}}