---
id: 822
title: 'Magento how to remove order'
date: '2013-08-11T19:38:44+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=822'
permalink: /index.php/2013/08/11/magento-how-to-remove-order/
snapEdIT:
    - '1'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/"     class="crp_title">Magento: Linking multiple shipments with their invoices</a></li><li><a href="http://ka.lpe.sh/2012/08/09/magento-how-to-delete-remove-all-products-from-all-categories/"     class="crp_title">Magento: How to delete/remove all products from all categories</a></li><li><a href="http://ka.lpe.sh/2012/07/24/mysql-delete-duplicate-records/"     class="crp_title">Mysql delete duplicate records leaving one</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-joining-groupby-order-invoice-shipment-tables/"     class="crp_title">Magento: Joining/group by &#8211; order, invoice, shipment tables</a></li></ul></div>'
snapFB:
    - 's:302:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:28:"1361121612_10200527513374601";s:5:"pDate";s:19:"2013-08-11 19:39:03";}}";'
snapTW:
    - 's:225:"a:1:{i:0;a:7:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"366644952823906307";s:5:"pDate";s:19:"2013-08-11 19:39:03";}}";'
snapLI:
    - 's:410:"a:1:{i:0;a:8:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:123:"http://www.linkedin.com/updates?discuss=&amp;scope=20008880&amp;stype=M&amp;topic=5772410668049260544&amp;type=U&amp;a=lqlK";s:5:"pDate";s:19:"2013-08-11 19:39:09";}}";'
categories:
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