---
id: 713
title: 'Magento get attribute label'
date: '2013-06-15T19:25:06+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=713'
permalink: /index.php/2013/06/15/magento-get-attribute-label/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li><li><a href="http://ka.lpe.sh/2013/06/15/magento-get-list-of-all-product-attributes/"     class="crp_title">Magento get list of all product attributes</a></li><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/"     class="crp_title">Magento: Get all the values of a Magento EAV for a particular attribute code</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-customer/"     class="crp_title">Magento add attribute to customer</a></li></ul></div>'
categories:
    - Magento
tags:
    - attribute
    - magento
---

To get attribute label for the product in Magento is not that straight-forward as we do for getting attribute value. You will need attribute code and product object to get the attribute label as shown below.

If you have the product object, you can use it to get the attribute’s label..  
{{< highlight php "style=emacs" >}}$label = $product->getResource()->getAttribute($attribute_code)->getFrontend()->getLabel($product);{{< /highlight >}}

For the current/selected store view..  
{{< highlight php "style=emacs" >}}$label = $product->getResource()->getAttribute($attribute_code)->getStoreLabel();{{< /highlight >}}

This will output you the label of the attribute associated with the attribute code you passed for that product. E.g. Shirt Size, Color, etc..

To get select/dropdown attribute label by value OR to get select/dropdown attribute value by label, please check this post: <http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/>