---
id: 708
title: 'Magento get list of all product attributes'
date: '2013-06-15T00:16:13+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - attribute
    - magento
    - product
---

Get list of all the product attributes defined in Magento. This will fetch you an array with all the attribute codes as a key AND all the attribute details including attribute code as a value. You can limit this array by just attribute code and attribute label as per your need. I will show you all the possible attribute information you can fetch defined for the product.

{{< highlight php "style=emacs" >}}$attrib_data = array(); $allAttributeCodes = array();  
$attributes = Mage::getResourceModel(‘catalog/product_attribute_collection’)->getItems();

foreach ($attributes as $attribute){  
 $attrib_data[$attribute->getAttributeCode()] = $attribute->getData();  
 //$allAttributeCodes[] = $attribute->getAttributeCode();  
}{{< /highlight >}}

*Sample Output:*  
{{< highlight plain "style=emacs" >}}Array(  
 [color] => Array  
 (  
 [entity_type_id] => 10  
 [attribute_code] => color  
 [attribute_model] =>  
 [backend_model] =>  
 [backend_type] => int  
 [backend_table] =>  
 [frontend_model] =>  
 [frontend_input] => select  
 [frontend_label] => Color  
 [frontend_class] =>  
 [source_model] =>  
 [is_required] => 0  
 [is_user_defined] => 1  
 [default_value] =>  
 [is_unique] => 0  
 [note] =>  
 [attribute_id] => 272  
 [frontend_input_renderer] =>  
 [is_global] => 1  
 [is_visible] => 1  
 [is_searchable] => 1  
 [is_filterable] => 1  
 [is_comparable] => 1  
 [is_visible_on_front] => 0  
 [is_html_allowed_on_front] => 0  
 [is_used_for_price_rules] => 1  
 [is_filterable_in_search] => 1  
 [used_in_product_listing] => 0  
 [used_for_sort_by] => 0  
 [is_configurable] => 1  
 [apply_to] => simple  
 [is_visible_in_advanced_search] => 1  
 [position] => 1  
 [is_wysiwyg_enabled] => 0  
 [is_used_for_promo_rules] => 1  
 )  
 [other_attribute_code] => Array  
 (  
 ….  
 )  
){{< /highlight >}}

Now you can easily access all the attribute information from the above array.