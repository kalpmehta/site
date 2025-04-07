---
id: 332
title: 'Magento: Get category object from category name'
date: '2012-09-13T14:53:09+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - 'get categories from attribute set'
    - 'get category object from name'
    - 'magento category object'
---

Although this is very weird, to get category object (id, entity_type_id, attribute_set_id, children, etc.) from category name, sometimes it may be useful. Below lines of code will help you in getting it.

{{< highlight php "style=emacs" >}}$cat = Mage::getResourceModel(‘catalog/category_collection’)->addFieldToFilter(‘name’, ‘Category_Name_Here’);  
print_r($cat->getData());{{< /highlight >}}

To get the category id from $cat object, simply use: {{< highlight php "style=emacs" >}}$cat->getFirstItem()->getEntityId();{{< /highlight >}} Beware, the name should only return one category else the above query will return first category id no matter how many categories are retrieved.