---
id: 1031
title: 'Magento 2 hello world module in 2 mins!'
date: '2015-12-23T00:08:50+00:00'
author: kalpesh
layout: post
tags:
    - Magento2
tags:
    - 'hello world'
    - magento2
    - 'sample module'
---

**Create Magento 2 hello world module in 2 minutes!**

To create a simple custom module in Magento2 which will give an output on frontend website from your module, follow below steps:

*Change to app/code directory where all the Magento2 module lives. Notice there are no codepools (core, community, local) under this directory like it used to be in Magento 1.x*  
{{< highlight http >}} cd app/code{{< /highlight >}}

*Create your company name directory*  
{{< highlight http >}} mkdir Hello{{< /highlight >}}

*Create you module name directory*  
{{< highlight http >}} mkdir Hello/World{{< /highlight >}}

*Create etc directory to hold module config file*  
{{< highlight http >}} mkdir Hello/World/etc{{< /highlight >}}

*module.xml file is required only to hold module name and it’s version*  
{{< highlight http >}} vi Hello/World/etc/module.xml{{< /highlight >}}  
{{< highlight xml "style=emacs" >}}<?xml version="1.0"??>
  
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nonamespaceschemalocation="../../../../../lib/internal/Magento/Framework/Module/etc/module.xsd">  
 <module name="Hello_World" setup_version="0.1.0"></module>  
</config>{{< /highlight >}}

*Register your module, this is required in all the modules. Only thing you will change is your module name (Hello_World)*  
{{< highlight http >}} vi Hello/World/registration.php{{< /highlight >}}  
{{< highlight php "style=emacs" >}}<?php \Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Hello_World',
    __DIR__
);{{< /highlight >}}

<em?>
Create frontend directory under etc to define frontend routes. We are creating this because we want to output something on frontend website.  
{{< highlight http >}} mkdir Hello/World/etc/frontend{{< /highlight >}}

*routes.xml is used to give your module a front name. Only thing you will be interested is <route> tag which holds frontName for the enclosed module name.</route>*  
{{< highlight http >}} vi Hello/World/etc/frontend/routes.xml{{< /highlight >}}  
{{< highlight xml "style=emacs" >}}<?xml version="1.0"??>
  
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nonamespaceschemalocation="../../../../../../lib/internal/Magento/Framework/App/etc/routes.xsd">  
 <router id="standard">  
 <route frontname="first" id="first">  
 <module name="Hello_World"></module>  
 </route>  
 </router>  
</config>{{< /highlight >}}

*Create Controller directory to hold your module’s controller files*  
{{< highlight http >}} mkdir Hello/World/Controller{{< /highlight >}}

*Create your controller directory, this will become part of the url after frontName*  
{{< highlight http >}} mkdir Hello/World/Controller/Hello{{< /highlight >}}

*Create controller file, notice there is no controller action in Magento2 Controller. This will again become part of the url and will call execute() method of the class.*  
{{< highlight http >}} vi Hello/World/Controller/Hello/World.php{{< /highlight >}}  
{{< highlight php "style=emacs" >}}<?php namespace Hello\World\Controller\Hello;
class World extends \Magento\Framework\App\Action\Action
{
    public function execute()
    {
        echo 'Hello world!';
    }
}{{< /highlight >}}

<em?>
Change directory to reach Magento 2 root directory  
{{< highlight http >}} cd ../../{{< /highlight >}}

*Enable your module, so an entry will go to app/etc/config.php file and cache will be cleared*  
{{< highlight http >}} bin/magento module:enable Hello_World{{< /highlight >}}

*This will add your module with it’s current version to DB table setup_module, without running this command you won’t see the changes of newly created module.*  
{{< highlight http >}} bin/magento setup:upgrade{{< /highlight >}}

Check your module in browser: <http://www.yourwebsite.com/first/hello/world>. If you have done everything correct, it should output “Hello world!”

![Magento 2 hello world module](http://ka.lpe.sh/uploads/2015/12/magento2-hello-world-module.png)