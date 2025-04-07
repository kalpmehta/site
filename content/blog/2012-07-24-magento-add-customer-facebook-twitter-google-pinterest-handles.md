---
id: 289
title: 'Magento: Add customer Facebook, Twitter, Google+, Pinterest handles'
date: '2012-07-24T16:57:41+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'facebook twitter pinterest google+ handles'
    - 'magento customer attributes'
    - 'magento social network'
---

It’s always a good idea to get as much information as you get from customer. Adding customer’s social networking usernames are common in most of the sites, which can allow you to post content to their wall regarding any purchase customer made. It helps you to get more visibility of your store in front of customer’s friends and whoever visits their page.

So, you will need to add these in database, so that it can reflect to the customer’s account:  
{{< highlight php "style=emacs" >}}$installer = $this;  
$installer->startSetup();  
$setup = new Mage_Eav_Model_Entity_Setup(‘core_setup’);  
$setup->addAttribute(‘customer’, ‘facebook’, array(  
 ‘label’ => ‘Facebook’,  
 ‘type’ => ‘varchar’,  
 ‘input’ => ‘text’,  
 ‘default’ => ”,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘unique’ => true,  
 ‘user_defined’ => true,  
));{{< /highlight >}}{{< highlight php "style=emacs" >}}  
$setup->addAttribute(‘customer’, ‘twitter’, array(  
 ‘label’ => ‘Twitter’,  
 ‘type’ => ‘varchar’,  
 ‘input’ => ‘text’,  
 ‘default’ => ”,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘unique’ => true,  
 ‘user_defined’ => true,  
));  
$setup->addAttribute(‘customer’, ‘Google+’, array(  
 ‘label’ => ‘Google+’,  
 ‘type’ => ‘varchar’,  
 ‘input’ => ‘text’,  
 ‘default’ => ”,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘unique’ => true,  
 ‘user_defined’ => true,  
));  
$setup->addAttribute(‘customer’, ‘Pinterest’, array(  
 ‘label’ => ‘Pinterest’,  
 ‘type’ => ‘varchar’,  
 ‘input’ => ‘text’,  
 ‘default’ => ”,  
 ‘visible’ => true,  
 ‘required’ => false,  
 ‘unique’ => true,  
 ‘user_defined’ => true,  
));  
$installer->endSetup();  
$installer->installEntities();{{< /highlight >}}

Once attributes are added to database, you can easily add HTML in the customer’s profile page where you want them to display.