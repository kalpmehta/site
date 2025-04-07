---
id: 796
title: 'Magento redirect from observer'
date: '2013-07-21T14:11:11+00:00'
author: kalpesh
layout: post

tags:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - magento
    - observer
    - redirect
---

Redirection in observer doesn’t work normally as it do in Blocks, templates and controllers. Also there is no standard code to redirect from observer that works in every situation.

You will need an argument to achieve redirect when using below code:  
{{< highlight php "style=emacs" >}}public function observingMethod(Varien_Event_Observer $observer)  
{  
 $observer->getRequest()->setParam(‘return_url’,$urlToRedirect);  
}{{< /highlight >}}  
Note that $observer object should have getRequest() method to make above code work. You may need to use $observer->getEvent()->getFront()->getRequest() otherwise, or simply var_dump/Mage::log $observer to get better idea what methods the object have.

Or you can use below code which is not recommended:  
{{< highlight php "style=emacs" >}}public function observingMethod() {  
 header(‘Location: ‘ . $urlToRedirect);  
 exit;  
}{{< /highlight >}}  
We don’t need any arguments using above method.

Another approach, again not recommended:  
{{< highlight php "style=emacs" >}}public function observingMethod(Varien_Event_Observer $observer)  
{  
 $response = $observer->getResponse();  
 //$response = Mage::app()->getFrontController()->getResponse();  
 $response->setRedirect($urlToRedirect);

 Mage::app()->getFrontController()->sendResponse();  
}{{< /highlight >}}