---
id: 918
title: 'Magento event observer for customer registration success'
date: '2014-08-21T21:00:10+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - customer
    - event
    - magento
    - observer
    - register
---

If you are looking for how to execute some code when customer successfully sign up in your website, you can use below code to check if the registration was successful. Note, this will NOT check if customer was registered from checkout page, if you are looking for that please go to this [post](http://ka.lpe.sh/2014/08/21/magento-check-customer-registered-checkout-page/).

In your xml file:  
{{< highlight xml "style=emacs" >}}  
<events>  
 <customer_register_success>  
 <observers>  
 <namespace_module_customer_register_success>  
 <type>singleton</type>  
 <class>Namespace_Module_Model_Observer</class>  
 <method>customerRegisterSuccess</method>  
 </namespace_module_customer_register_success>  
 </observers>  
 </customer_register_success>  
</events>  
{{< /highlight >}}

And in your Observer.php file:  
{{< highlight php "style=emacs" >}}  
class Namespace_Module_Model_Observer {  
 public function customerRegisterSuccess(Varien_Event_Observer $observer) {  
 $event = $observer->getEvent();  
 $customer = $event->getCustomer();  
 $email = $customer->getEmail();  
 if($email) {  
 //code to handle if customer is successfully registered  
 }  
 }  
}  
{{< /highlight >}}