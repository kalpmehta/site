---
id: 822
title: 'Magento how to remove order'
date: '2013-08-11T19:38:44+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - magento
    - order
    - remove
---

First of all, removing live orders is not recommended. But if you are sure you want to remove orders (test orders?) then you can do so by custom script below. Get the order increment id(s) of the order you wish to delete from Magento. Remember, once order is deleted you can’t get any related information of that order.

Create a test PHP file in your Magento project root with below code:  
{{< highlight php "style=emacs" >}}require ‘app/Mage.php’;  
Mage::app(‘admin’)->setUseSessionInUrl(false);

$orderIncrementIDs = array(‘100000001′,’100000002’); //your order increment ids to delete, beware!  
$rmvd = array();

foreach($orderIncrementIDs as $ordID){  
 try{  
 Mage::getModel(‘sales/order’)->loadByIncrementId($ordID)->delete();  
 $rmvd[] = $ordID;  
 } catch(Exception $e){  
 echo ‘Error: ‘.$e->getMessage().’  
‘;  
 }  
}  
echo “Following Orders Removed!  
” . implode(“, “,$rmvd);{{< /highlight >}}  
and run the file to delete the order(s).  
  
You can also delete orders directly from database using below query:  
{{< highlight mariadb "style=emacs" >}}select @order_id:=entity_id from sales_order_entity where increment_id=’100000001′;  
delete from sales_order_entity where entity_id=@order_id or parent_id=@order_id;{{< /highlight >}}