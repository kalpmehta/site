---
id: 289
title: 'Magento: Add customer Facebook, Twitter, Google+, Pinterest handles'
date: '2012-07-24T16:57:41+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=289'
permalink: /index.php/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-order/"     class="crp_title">Magento add attribute to order</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2012/07/26/magento-check-if-customer-already-exist-or-not/"     class="crp_title">Magento: Check if customer already exist or not</a></li><li><a href="http://ka.lpe.sh/2013/01/04/magento-certification-preparation-interview-questions-answers/"     class="crp_title">Magento Certification Preparation / Interview Questions Answers</a></li></ul></div>'
categories:
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