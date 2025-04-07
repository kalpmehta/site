---
id: 920
title: 'Magento event to check if customer have subscribed to newsletter'
date: '2014-08-21T21:07:38+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - event
    - magento
    - newsletter
    - observer
    - subscribed
---

Check if the customer has subscribed to the newsletter from registration page or checkout page by using event observer. You may need to take some action programatically if customer subscribes to newsletter, below code will help you exactly in that.

Code to put in your config.xml  
{{< highlight xml "style=emacs" >}}  
<newsletter_subscriber_save_after>  
 <observers>  
 <namespace_module_model_observer>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>subscribedToNewsletter</method>  
 </namespace_module_model_observer>  
 </observers>  
</newsletter_subscriber_save_after>  
{{< /highlight >}}

Code to put in your Observer.php file  
{{< highlight php "style=emacs" >}}  
class Namespace_Module_Model_Observer {  
 public function subscribedToNewsletter(Varien_Event_Observer $observer)  
 {  
 $event = $observer->getEvent();  
 $subscriber = $event->getDataObject();  
 $data = $subscriber->getData();  
 $email = $data[‘subscriber_email’];

 $statusChange = $subscriber->getIsStatusChanged();  
 if ($data[‘subscriber_status’] == “1” &amp;&amp; $statusChange == true) {  
 //code to handle if customer is just subscribed…  
 }  
 }  
}  
{{< /highlight >}}