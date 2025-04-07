---
id: 713
title: 'Magento get attribute label'
date: '2013-06-15T19:25:06+00:00'
author: kalpesh
layout: post
tags:
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