---
id: 327
title: 'Magento: Get product attribute&#8217;s select option id/label/value'
date: '2012-09-13T13:04:16+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'get attribute option id value label'
    - 'magento get attribute label from value id'
    - 'magento get attribute value from label'
---

If you have a select dropdown for any product attribute, to get the value from label or vice versa is always needed in order to display or get value for further processing, etc. Every now and then you will require this values while working on product attributes. There aer many ways you can achieve it but the best, in terms of performance and simplicity is what I will tell you here. Get product attribute’s value from label, label from value easily in Magento.

Suppose, you have an product attribute called “color” in Magento. You have the label (e.g. Red), and you want to find it’s value. The below code will help you get the value for it.  
{{< highlight php "style=emacs" >}}$productModel = Mage::getModel(‘catalog/product’);  
$attr = $productModel->getResource()->getAttribute(“color”);  
if ($attr->usesSource()) {  
 echo $color_id = $attr->getSource()->getOptionId(“Red”);  
}{{< /highlight >}}  
  
Now suppose, you have the value (let’s say 8, for Red) for your attribute, but want to get the label for it. Below code will help you to achive it.

{{< highlight php "style=emacs" >}}$productModel = Mage::getModel(‘catalog/product’);  
$attr = $productModel->getResource()->getAttribute(“color”);  
if ($attr->usesSource()) {  
 echo $color_label = $attr->getSource()->getOptionText(“8”);  
}{{< /highlight >}}

Note that the only thing changed in both is, getOptionId() and getOptionText. getOptionId() will accept label and give you value, while getOptionText() will accept value and give you label.