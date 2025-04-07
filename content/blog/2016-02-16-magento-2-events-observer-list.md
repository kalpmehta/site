---
id: 1060
title: 'Magento 2 events observer list'
date: '2016-02-16T21:54:49+00:00'
author: kalpesh
layout: post
tags:
    - Magento2
tags:
    - event
    - magento2
    - observer
---

Below is a list of all the events dispatched that you can observe in your Magento 2 web store.

**Magento 2 Events Observer list:**

{{< highlight http >}}   
‘adminhtml_cache_flush_all’  
‘adminhtml_cache_flush_system’  
‘backend_auth_user_login_success’, [‘user’ => $this->getCredentialStorage()]  
‘backend_auth_user_login_failed’, [‘user_name’ => $username, ‘exception’ => $e]  
‘backend_auth_user_login_failed’, [‘user_name’ => $username, ‘exception’ => $e]  
‘adminhtml_store_edit_form_prepare_form’, [‘block’ => $this]  
‘adminhtml_block_html_before’, [‘block’ => $this]  
‘backend_block_widget_grid_prepare_grid_before’, [‘grid’ => $this, ‘collection’ => $this->getCollection()]  
‘theme_save_after’  
‘store_group_save’, [‘group’ => $groupModel]  
‘store_delete’, [‘store’ => $model]  
‘adminhtml_cache_flush_system’  
‘clean_media_cache_after’  
‘clean_static_files_cache_after’  
‘adminhtml_cache_flush_all’  
‘clean_catalog_images_cache_after’  
‘sales_quote_item_qty_set_after’, [‘item’ => $this]  
‘sales_quote_item_set_product’, [‘product’ => $product, ‘quote_item’ => $this]  
‘sales_quote_collect_totals_before’, [‘quote’ => $quote]  
‘sales_quote_collect_totals_after’, [‘quote’ => $quote]  
‘sales_quote_address_collect_totals_before’, [  
‘sales_quote_address_collect_totals_after’, [  
$this->_eventPrefix . ‘_import_data_before’, [$this->_eventObject => $this, ‘input’ => $data]  
‘sales_convert_quote_to_order’, [‘order’ => $order, ‘quote’ => $object->getQuote()]  
‘items_additional_data’, [‘item’ => $item]  
‘checkout_submit_before’, [‘quote’ => $quote]  
‘checkout_submit_all_after’, [‘order’ => $order, ‘quote’ => $quote]  
‘sales_model_service_quote_submit_before’, [  
‘sales_model_service_quote_submit_success’, [  
‘sales_model_service_quote_submit_failure’, [  
‘prepare_catalog_product_collection_prices’, [‘collection’ => $productCollection, ‘store_id’ => $this->getStoreId()]  
‘sales_quote_item_collection_products_after_load’, [‘collection’ => $productCollection]  
$this->_eventPrefix . ‘_load_after’, [$this->_eventObject => $this]  
‘sales_quote_remove_item’, [‘quote_item’ => $item]  
‘sales_quote_add_item’, [‘quote_item’ => $item]  
‘sales_quote_product_add_after’, [‘items’ => $items]  
$this->_eventPrefix . ‘_merge_before’, [$this->_eventObject => $this, ‘source’ => $quote]  
$this->_eventPrefix . ‘_merge_after’, [$this->_eventObject => $this, ‘source’ => $quote]  
‘salesrule_validator_process’, [  
‘sales_quote_address_discount_item’, $eventArgs  
‘sales_quote_address_discount_item’, $eventArgs  
‘salesrule_rule_get_coupon_types’, [‘transport’ => $transport]  
‘salesrule_rule_condition_combine’, [‘additional’ => $additional]  
‘adminhtml_promo_quote_edit_tab_main_prepare_form’, [‘form’ => $form]  
‘adminhtml_promo_quote_edit_tab_coupons_form_prepare_form’, [‘form’ => $form]  
‘adminhtml_block_salesrule_actions_prepareform’, [‘form’ => $form]  
‘adminhtml_block_promo_widget_chooser_prepare_collection’, [‘collection’ => $collection]  
‘adminhtml_controller_salesrule_prepare_save’, [‘request’ => $this->getRequest()]  
‘clean_cache_by_tags’, [‘object’ => $this->cacheContext]  
‘paypal_express_place_order_success’, [  
‘catalog_product_validate_variations_before’, [‘product’ => $parentProduct, ‘variations’ => $products]  
‘rss_catalog_review_collection_select’, [‘collection’ => $collection]  
‘review_review_collection_load_before’, [‘collection’ => $this]  
‘rating_rating_collection_load_before’, [‘collection’ => $this]  
‘review_controller_product_init_before’, [‘controller_action’ => $this]  
‘review_controller_product_init’, [‘product’ => $product]  
‘review_controller_product_init_after’, [‘product’ => $product, ‘controller_action’ => $this]  
‘wishlist_item_collection_products_after_load’, [‘product_collection’ => $productCollection]  
‘wishlist_add_item’, [‘item’ => $item]  
‘wishlist_product_add_after’, [‘items’ => $items]  
‘rss_wishlist_xml_callback’, $args  
‘product_option_renderer_init’, [‘block’ => $this]  
‘wishlist_add_product’, [‘wishlist’ => $wishlist, ‘product’ => $product, ‘item’ => $result]  
‘wishlist_share’, [‘wishlist’ => $wishlist]  
‘wishlist_update_item’, [‘wishlist’ => $wishlist, ‘product’ => $product, ‘item’ => $wishlist->getItem($id)]  
‘wishlist_items_renewed’  
‘catalog_product_prepare_index_select’, [  
‘prepare_catalog_product_collection_prices’, [‘collection’ => $selections, ‘store_id’ => $product->getStoreId()]  
‘catalog_product_get_final_price’, [‘product’ => $product, ‘qty’ => $qty]  
‘catalog_product_get_final_price’, [‘product’ => $product, ‘qty’ => $bundleQty]  
‘catalog_product_option_price_configuration_after’, [‘configObj’ => $configObj]  
‘catalog_product_get_final_price’, [‘product’ => $product, ‘qty’ => $this->bundleProduct->getQty()]  
$this->_eventPrefix . ‘_move_before’, $eventParams  
$this->_eventPrefix . ‘_move_after’, $eventParams  
‘category_move’, $eventParams  
‘catalog_category_change_products’, [‘category’ => $category, ‘product_ids’ => $productIds]  
$this->_eventPrefix . ‘_load_before’, [$this->_eventObject => $this]  
$this->_eventPrefix . ‘_load_after’, [$this->_eventObject => $this]  
$this->_eventPrefix . ‘_add_is_active_filter’, [$this->_eventObject => $this]  
‘catalog_category_tree_init_inactive_category_ids’, [‘tree’ => $this]  
‘catalog_category_flat_loadnodes_before’, [‘select’ => $select]  
‘catalog_category_tree_init_inactive_category_ids’, [‘tree’ => $this]  
$this->_eventPrefix . ‘_load_before’, [$this->_eventObject => $this]  
$this->_eventPrefix . ‘_load_after’, [$this->_eventObject => $this]  
$this->_eventPrefix . ‘_add_is_active_filter’, [$this->_eventObject => $this]  
‘catalog_product_delete_after_done’, [‘product’ => $object]  
‘prepare_catalog_product_index_select’, [  
‘catalog_prepare_price_select’, $eventArgs  
‘catalog_product_collection_load_after’, [‘collection’ => $this]  
‘catalog_product_collection_before_add_count_to_categories’, [‘collection’ => $this]  
‘catalog_product_collection_apply_limitations_after’, [‘collection’ => $this]  
‘catalog_product_compare_item_collection_clear’  
$this->_eventPrefix . ‘_validate_before’, $this->_getEventData()  
$this->_eventPrefix . ‘_validate_after’, $this->_getEventData()  
‘catalog_product_is_salable_before’, [‘product’ => $this]  
‘catalog_product_is_salable_after’, [‘product’ => $this, ‘salable’ => $object]  
$eventName, [‘transport’ => $transport, ‘buy_request’ => $buyRequest, ‘product’ => $product]  
‘catalog_product_get_final_price’, [‘product’ => $product, ‘qty’ => $qty]  
‘catalog_product_attribute_update_before’, [‘attributes_data’ => &amp;$attrData, ‘product_ids’ => &amp;$productIds, ‘store_id’ => &amp;$storeId]  
‘adminhtml_product_attribute_types’, [‘response’ => $response]  
‘rss_catalog_notify_stock_collection_select’, [‘collection’ => $collection]  
‘clean_cache_by_tags’, [‘object’ => $this->cacheContext]  
‘adminhtml_catalog_category_tabs’, [‘tabs’ => $this]  
‘adminhtml_catalog_category_edit_prepare_form’, [‘form’ => $form]  
‘adminhtml_catalog_category_tree_is_moveable’, [‘options’ => $options]  
‘adminhtml_catalog_category_tree_can_add_root_category’, [‘category’ => $this->getCategory(), ‘options’ => $options, ‘store’ => $this->getStore()->getId()]  
‘adminhtml_catalog_category_tree_can_add_sub_category’, [‘category’ => $this->getCategory(), ‘options’ => $options, ‘store’ => $this->getStore()->getId()]  
‘adminhtml_catalog_product_grid_prepare_massaction’, [‘block’ => $this]  
‘catalog_product_gallery_prepare_layout’, [‘block’ => $this]  
‘product_attribute_grid_build’, [‘grid’ => $this]  
‘adminhtml_catalog_product_attribute_set_toolbar_main_html_before’, [‘block’ => $this]  
‘adminhtml_catalog_product_attribute_set_main_html_before’, [‘block’ => $this]  
‘adminhtml_catalog_product_edit_prepare_form’, [‘form’ => $form]  
‘adminhtml_catalog_product_edit_element_types’, [‘response’ => $response]  
‘adminhtml_product_attribute_types’, [‘response’ => $response]  
‘product_attribute_form_build_main_tab’, [‘form’ => $form]  
‘product_attribute_form_build_front_tab’, [‘form’ => $form]  
‘adminhtml_catalog_product_attribute_edit_frontend_prepare_form’, [‘form’ => $form, ‘attribute’ => $attributeObject]  
‘product_attribute_form_build’, [‘form’ => $form]  
‘adminhtml_catalog_product_form_prepare_excluded_field_list’, [‘object’ => $this]  
‘adminhtml_catalog_product_edit_tab_attributes_create_html_before’, [‘block’ => $this]  
‘adminhtml_catalog_product_edit_prepare_form’, [‘form’ => $form, ‘layout’ => $this->getLayout()]  
‘adminhtml_catalog_product_edit_element_types’, [‘response’ => $response]  
‘shortcut_buttons_container’, [  
‘catalog_product_view_config’, [‘response_object’ => $responseObject]  
‘catalog_product_upsell’, [‘product’ => $product, ‘collection’ => $this->_itemCollection, ‘limit’ => null]  
‘catalog_block_product_list_collection’, [‘collection’ => $this->_getProductCollection()]  
‘catalog_product_option_price_configuration_after’, [‘configObj’ => $configObj]  
‘catalog_block_product_status_display’, [‘status’ => $statusInfo]  
‘rss_catalog_category_xml_callback’, [‘product’ => $product]  
‘rss_catalog_new_xml_callback’, [‘row’ => $item->getData(), ‘product’ => $item  
‘rss_catalog_special_xml_callback’, [‘row’ => $item->getData(), ‘product’ => $item  
‘catalog_category_prepare_save’, [‘category’ => $category, ‘request’ => $this->getRequest()]  
‘category_prepare_ajax_response’, [‘response’ => $eventResponse, ‘controller’ => $this]  
‘catalog_controller_category_delete’, [‘category’ => $category]  
‘catalog_product_to_website_change’, [‘products’ => $productIds]  
‘controller_action_catalog_product_save_entity_after’, [‘controller’ => $this]  
‘catalog_product_edit_action’, [‘product’ => $product]  
‘catalog_product_new_action’, [‘product’ => $product]  
‘catalog_product_gallery_upload_image_after’, [‘result’ => $result, ‘action’ => $this]  
‘catalog_controller_category_init_after’, [‘category’ => $category, ‘controller_action’ => $this]  
‘catalog_product_compare_remove_product’, [‘product’ => $item]  
‘catalog_product_compare_add_product’, [‘product’ => $product]  
‘catalog_controller_product_init_before’, [‘controller_action’ => $controller, ‘params’ => $params]  
‘catalog_controller_product_init_after’, [‘product’ => $product, ‘controller_action’ => $controller]  
‘catalog_controller_product_view’, [‘product’ => $product]  
‘assign_theme_to_stores_after’, [‘stores’ => $stores, ‘scope’ => $scope, ‘theme’ => $theme]  
‘page_block_html_topmenu_gethtml_before’, [‘menu’ => $this->_menu, ‘block’ => $this]  
‘page_block_html_topmenu_gethtml_after’, [‘menu’ => $this->_menu, ‘transportObject’ => $transportObject]  
‘gift_options_prepare_items’, [‘items’ => $entityItems]  
‘adminhtml_cache_refresh_type’  
‘depersonalize_clear_session’  
‘customer_session_init’, [‘customer_session’ => $this]  
‘customer_login’, [‘customer’ => $customer]  
‘customer_data_object_login’, [‘customer’ => $this->getCustomerDataObject()]  
‘customer_data_object_login’, [‘customer’ => $customer]  
‘customer_logout’, [‘customer’ => $this->getCustomer()]  
‘customer_customer_authenticated’, [‘model’ => $this, ‘password’ => $password]  
‘customer_validate’, [‘customer’ => $this, ‘transport’ => $transport]  
‘customer_customer_authenticated’, [‘model’ => $customerModel, ‘password’ => $password]  
‘customer_data_object_login’, [‘customer’ => $customer]  
‘customer_save_after_data_object’, [‘customer_data_object’ => $savedCustomer, ‘orig_customer_data_object’ => $customer]  
‘visitor_init’, [‘visitor’ => $this]  
‘visitor_activity_save’, [‘visitor’ => $this]  
‘customer_address_format’, [‘type’ => $formatType, ‘address’ => $this]  
‘adminhtml_block_html_before’, [‘block’ => $this]  
‘customer_register_success’, [‘account_controller’ => $this, ‘customer’ => $customer]  
‘adminhtml_customer_prepare_save’, [‘customer’ => $customer, ‘request’ => $request]  
‘adminhtml_customer_save_after’, [‘customer’ => $customer, ‘request’ => $request]  
‘catalog_product_prepare_index_select’, [  
‘on_view_report’, [‘report’ => ‘search’]  
‘sales_prepare_amount_expression’, [‘collection’ => $this, ‘expression_object’ => $expressionTransferObject]  
‘adminhtml_widget_grid_filter_collection’, [‘collection’ => $this->getCollection(), ‘filter_values’ => $this->_filterValues]  
‘clean_cache_after_reindex’, [‘object’ => $this->context]  
‘checkout_type_multishipping_set_shipping_items’, [‘quote’ => $quote]  
‘checkout_type_multishipping_create_orders_single’, [‘order’ => $order, ‘address’ => $address, ‘quote’ => $this->getQuote()]  
‘checkout_submit_all_after’, [‘orders’ => $orders, ‘quote’ => $this->getQuote()]  
‘checkout_multishipping_refund_all’, [‘orders’ => $orders]  
‘multishipping_checkout_controller_success_action’, [‘order_ids’ => $ids]  
‘checkout_controller_multishipping_shipping_post’, [‘request’ => $this->getRequest(), ‘quote’ => $this->_getCheckout()->getQuote()]  
‘persistent_session_expired’  
‘adminhtml_cms_page_edit_tab_main_prepare_form’, [‘form’ => $form]  
‘adminhtml_cms_page_edit_tab_design_prepare_form’, [‘form’ => $form]  
‘adminhtml_cms_page_edit_tab_content_prepare_form’, [‘form’ => $form]  
‘adminhtml_cms_page_edit_tab_meta_prepare_form’, [‘form’ => $form]  
‘cms_controller_router_match_before’, [‘router’ => $this, ‘condition’ => $condition]  
‘cms_page_prepare_save’, [‘page’ => $model, ‘request’ => $this->getRequest()]  
‘adminhtml_cmspage_on_delete’, [‘title’ => $title, ‘status’ => ‘success’]  
‘adminhtml_cmspage_on_delete’, [‘title’ => $title, ‘status’ => ‘fail’]  
‘cms_page_render’, [‘page’ => $this->_page, ‘controller_action’ => $action]  
‘cms_wysiwyg_images_static_urls_allowed’, [‘result’ => $checkResult, ‘store_id’ => $this->_storeId]  
‘sales_order_place_before’, [‘order’ => $this]  
‘sales_order_place_after’, [‘order’ => $this]  
‘order_cancel_after’, [‘order’ => $this]  
‘sales_convert_order_to_quote’, [‘order’ => $order, ‘quote’ => $quote]  
‘sales_convert_order_item_to_quote_item’, [‘order_item’ => $orderItem, ‘quote_item’ => $item]  
‘checkout_submit_all_after’, [‘order’ => $order, ‘quote’ => $quote]  
‘sales_order_status_unassign’, [  
’email_invoice_comment_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_invoice_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_order_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_shipment_comment_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_shipment_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_creditmemo_comment_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_creditmemo_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
’email_order_comment_set_template_vars_before’, [‘sender’ => $this, ‘transport’ => $transport]  
‘sales_order_item_cancel’, [‘item’ => $this]  
‘sales_order_payment_place_start’, [‘payment’ => $this]  
‘sales_order_payment_place_end’, [‘payment’ => $this]  
‘sales_order_payment_pay’, [‘payment’ => $this, ‘invoice’ => $invoice]  
‘sales_order_payment_cancel_invoice’, [‘payment’ => $this, ‘invoice’ => $invoice]  
‘sales_order_payment_void’, [‘payment’ => $this, ‘invoice’ => $document]  
‘sales_order_payment_refund’, [‘payment’ => $this, ‘creditmemo’ => $creditmemo]  
‘sales_order_payment_cancel_creditmemo’, [‘payment’ => $this, ‘creditmemo’ => $creditmemo]  
‘sales_order_payment_cancel’, [‘payment’ => $this]  
‘sales_order_invoice_pay’, [$this->_eventObject => $this]  
‘sales_order_invoice_cancel’, [$this->_eventObject => $this]  
‘sales_order_invoice_register’, [$this->_eventObject => $this, ‘order’ => $order]  
$this->_eventPrefix . ‘_html_txn_id’, $this->_getEventData()  
‘sales_order_payment_capture’, [‘payment’ => $payment, ‘invoice’ => $invoice]  
‘customer_address_format’, [‘type’ => $formatType, ‘address’ => $address]  
$this->_eventPrefix . ‘_set_sales_order’, [‘collection’ => $this, $this->_eventObject => $this, ‘order’ => $order]  
$this->_eventPrefix . ‘_load_after’, [$this->_eventObject => $this]  
‘sales_sale_collection_query_before’, [‘collection’ => $this]  
$object->getEventPrefix() . ‘_save_attribute_before’, [  
$object->getEventPrefix() . ‘_save_attribute_after’, [  
‘sales_order_state_change_before’, [‘order’ => $this, ‘transport’ => $transport]  
‘sales_order_creditmemo_cancel’, [‘creditmemo’ => $creditmemo]  
‘sales_order_creditmemo_refund’, [‘creditmemo’ => $creditmemo]  
$this->_eventPrefix . ‘_sales_email_general_async_sending_’ . $state,  
$this->_eventPrefix . ‘_dev_grid_async_indexing_’ . $state,  
‘rss_order_new_collection_select’, [‘collection’ => $collection]  
‘adminhtml_customer_orders_add_action_renderer’, [‘renderer’ => $this, ‘row’ => $row]  
‘adminhtml_sales_order_creditmemo_register_before’, [‘creditmemo’ => $creditmemo, ‘input’ => $this->getCreditmemo()]  
‘adminhtml_sales_order_create_process_data_before’, $eventData  
‘admin_sales_order_address_update’, [  
‘tax_rate_data_fetch’, [‘request’ => $request, ‘sender’ => $this]  
‘tax_settings_change_after’  
‘adminhtml_cache_refresh_type’, [‘type’ => ‘block_html’]  
‘checkout_type_onepage_save_order_after’, [‘order’ => $order, ‘quote’ => $this->getQuote()]  
‘checkout_submit_all_after’, [  
‘custom_quote_process’, [‘checkout_session’ => $this]  
‘checkout_quote_init’, [‘quote’ => $quote]  
‘load_customer_quote_before’, [‘checkout_session’ => $this]  
‘checkout_quote_destroy’, [‘quote’ => $this->getQuote()]  
‘restore_quote’, [‘order’ => $order, ‘quote’ => $quote]  
‘checkout_cart_product_add_after’, [‘quote_item’ => $result, ‘product’ => $product]  
‘checkout_cart_update_items_before’, [‘cart’ => $this, ‘info’ => $infoDataObject]  
‘checkout_cart_update_items_after’, [‘cart’ => $this, ‘info’ => $infoDataObject]  
‘checkout_cart_save_before’, [‘cart’ => $this]  
‘checkout_cart_save_after’, [‘cart’ => $this]  
‘checkout_cart_product_update_after’, [‘quote_item’ => $result, ‘product’ => $product]  
‘shortcut_buttons_container’, [  
‘checkout_cart_add_product_complete’, [‘product’ => $product, ‘request’ => $this->getRequest(), ‘response’ => $this->getResponse()]  
‘checkout_cart_update_item_complete’, [‘item’ => $item, ‘request’ => $this->getRequest(), ‘response’ => $this->getResponse()]  
‘checkout_onepage_controller_success_action’, [‘order_ids’ => [$session->getLastOrderId()]]  
‘checkout_controller_onepage_saveOrder’, [  
‘checkout_allow_guest’, [‘quote’ => $quote, ‘store’ => $store, ‘result’ => $result]  
‘controller_action_nocookies’, [‘action’ => $this, ‘redirect’ => $redirect]  
‘eav_collection_abstract_load_before’, [‘collection’ => $this]  
‘adminhtml_block_eav_attribute_edit_form_init’, [‘form’ => $this->getForm()]  
‘sendfriend_product’, [‘product’ => $product]  
‘catalog_product_import_bunch_delete_after’, [‘adapter’ => $this, ‘bunch’ => $bunch]  
‘catalog_product_import_finish_before’, [‘adapter’ => $this]  
‘catalog_product_import_bunch_save_after’, [‘adapter’ => $this, ‘bunch’ => $bunch]  
‘admin_user_authenticate_before’, [‘username’ => $username, ‘user’ => $this]  
‘admin_user_authenticate_after’, [‘username’ => $username, ‘password’ => $password, ‘user’ => $this, ‘result’ => $result]  
‘permissions_role_html_before’, [‘block’ => $this]  
‘admin_permissions_role_prepare_save’, [‘object’ => $role, ‘request’ => $this->getRequest()]  
‘store_address_format’, [‘type’ => $type, ‘store_info’ => $storeInfo]  
‘swatch_gallery_upload_image_after’, [‘result’ => $result, ‘action’ => $this]  
‘payment_method_is_active’, [  
‘payment_method_assign_data_’ . $this->getCode(), [  
‘payment_cart_collect_items_and_amounts’, [‘cart’ => $this]  
‘payment_form_block_to_html_before’, [‘block’ => $this]  
‘catelogsearch_searchable_attributes_load_after’, [‘engine’ => $this->engine, ‘attributes’ => $attributes]  
‘catelogsearch_searchable_attributes_load_after’, [‘engine’ => $this->engine, ‘attributes’ => $attributes]  
‘catalogsearch_reset_search_result’  
‘checkout_directpost_placeOrder’, [  
‘clean_cache_by_tags’, [‘object’ => $this]  
‘adminhtml_promo_catalog_edit_tab_main_prepare_form’, [‘form’ => $form]  
‘adminhtml_controller_catalogrule_prepare_save’, [‘request’ => $this->getRequest()]  
“admin_system_config_changed_section_{$this->getSection()}”, [‘website’ => $this->getWebsite(), ‘store’ => $this->getStore()]  
‘adminhtml_system_config_advanced_disableoutput_render_before’, [‘modules’ => $dispatchResult]  
‘admin_system_config_changed_section_currency_before_reinit’, [‘website’ => $this->_websiteId, ‘store’ => $this->_storeId]  
‘admin_system_config_changed_section_currency’, [‘website’ => $this->_websiteId, ‘store’ => $this->_storeId]{{< /highlight >}}