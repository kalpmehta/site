---
id: 32
title: 'Magento 1.5: Cannot login to admin panel after fresh install'
date: '2011-06-05T07:11:19+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento error'
tags:
    - error
    - magento
---

After installing magento 1.5, I tried to login to the admin panel with correct username and password, but it does not let me in without any error message. This is due to cookie problem in magento and can be fixed as below:

Open this file in your favorite editor: **app/code/core/Mage/Core/Model/Session/Abstract/Varien.php**

Comment lines that says like (probably line number 81 to 83)  
{{< highlight php "style=emacs" >}}  
$this->getCookie()->getDomain(),  
$this->getCookie()->isSecure(),  
$this->getCookie()->getHttponly()  
{{< /highlight >}}  
to  
{{< highlight php "style=emacs" >}}  
//$this->getCookie()->getDomain(),  
//$this->getCookie()->isSecure(),  
//$this->getCookie()->getHttponly()  
{{< /highlight >}}  
Now you could login to your admin panel without any problem.