---
id: 270
title: 'Magento add radio / checkbox button to admin grid'
date: '2012-07-12T16:27:34+00:00'
author: kalpesh
layout: post
tags:
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