---
id: 270
title: 'Magento add radio / checkbox button to admin grid'
date: '2012-07-12T16:27:34+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=270'
permalink: /index.php/2012/07/12/magento-add-radio-checkbox-button-to-admin-grid/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2013/02/26/magento-cant-see-product-images-in-category-page/"     class="crp_title">Magento: Can&#8217;t see product images in category page</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - add
    - 'admin grid'
    - checkbox
    - magento
    - radio
---

Add custom column in admin Grid which will show radio/checkbox button. I know this is weird, but some people need this as a requirement. Here I will show you how you can have radio button or checkbox button that you can have directly in your grids.

For radio button,  
{{< highlight php "style=emacs" >}}$this->addColumn(‘some_id’, array(  
 ‘header_css_class’ => ‘a-center’,  
 ‘header’ => Mage::helper(‘adminhtml’)->__(‘Some Header’),  
 ‘type’ => ‘radio’,  
 ‘html_name’ => ‘items[]’,  
 ‘align’ => ‘center’,  
 ‘value’ => array(‘1’)  
 ));{{< /highlight >}}  
  
For checkbox button,  
{{< highlight php "style=emacs" >}}$this->addColumn(‘some_id’, array(  
 ‘header_css_class’ => ‘a-center’,  
 ‘header’ => Mage::helper(‘adminhtml’)->__(‘Some Header’),  
 ‘type’ => ‘radio’,  
 ‘field_name’ => ‘items[]’,  
 ‘align’ => ‘center’,  
 ‘values’ => array(‘1′,’2’)  
 ));{{< /highlight >}}

Further, in Form.php you can add this below code to have by default behavior and onclick behaviour:  
{{< highlight php "style=emacs" >}}$fieldset->addField(‘some_id’, ‘checkbox’, array(  
 ‘checked’ => $this->getSomeId()==1 ? ‘true’ : ‘false’,  
 ‘onclick’ => ‘this.value = this.checked ? 1 : 0;’  
)); {{< /highlight >}}

Hope this helps some frustrated mind!