---
id: 332
title: 'Magento: Get category object from category name'
date: '2012-09-13T14:53:09+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=332'
permalink: /index.php/2012/09/13/magento-get-category-object-from-category-name/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-add-attribute-to-category/"     class="crp_title">Magento add attribute to category</a></li><li><a href="http://ka.lpe.sh/2012/02/29/php-convert-simplexml-to-array/"     class="crp_title">PHP Convert SimpleXML object to Array</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li></ul></div>'
categories:
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