---
id: 256
title: 'Magento: Difference between order states and statuses'
date: '2012-04-21T16:47:38+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=256'
permalink: /index.php/2012/04/21/magento-order-state-vs-status/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-getting-back-shopping-cart-items-after-order-fails/"     class="crp_title">Magento: Getting back shopping cart items after order fails</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento Interview'
tags:
    - difference
    - magento
    - order
    - state
    - status
    - versus
---

If you are building website in Magento, you may have noticed that there are two columns in *sales_flat_order* table which are confusing. These are **state** and **status**. You might think what is the difference between these two, both having same meaning.

Well, this is not the case. They both are different. State is used by magento to tell if the order is new, processing, complete, holded, closed, canceled, etc.; while Statuses are the one that YOU would be defining at the backend in System -> Order Statuses. Magento displays order STATUSES and not STATES in the backend order detail page to let you know which status is assigned as per your mapping. Remember, multiple statuses can be mapped with one state, while vice versa is not possible.

Consider an example, your customer places an order as Cash on Delivery, you will need something like COD_Pending as the order status so that you know it is not yet paid. Magento will have state *new* for this, which makes you unpredictable of what kind of transaction is this, COD or Prepaid. The STATUS can be anything, as you define, for your understanding; while STATE is something which Magento needs to understand, internally.

In short, Magento uses order state internally for processing order, whereas order status are used by store owners to understand the exact order flow where one state can be assigned to multiple statuses.

To understand this in detail, have a look at [this](http://www.magentocommerce.com/wiki/2_-_magento_concepts_and_architecture/order_management)  
Hope it helps!