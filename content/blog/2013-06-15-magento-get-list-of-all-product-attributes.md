---
id: 708
title: 'Magento get list of all product attributes'
date: '2013-06-15T00:16:13+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=708'
permalink: /index.php/2013/06/15/magento-get-list-of-all-product-attributes/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/24/magento-add-additional-product-item-attributes-in-order-and-invoice-emails/"     class="crp_title">Magento: Add additional product/item attributes in order and invoice emails</a></li><li><a href="http://ka.lpe.sh/2013/02/07/magento-add-product-custom-attribute-options-dynamically/"     class="crp_title">Magento: Add product custom attribute options dynamically</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2011/06/06/magento-get-all-the-values-of-a-magento-eav-for-a-particular-attribute-code/"     class="crp_title">Magento: Get all the values of a Magento EAV for a particular attribute code</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li></ul></div>'
categories:
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