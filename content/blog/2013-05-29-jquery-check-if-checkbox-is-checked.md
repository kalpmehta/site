---
id: 674
title: 'jQuery check if checkbox is checked or not'
date: '2013-05-29T11:49:19+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=674'
permalink: /index.php/2013/05/29/jquery-check-if-checkbox-is-checked/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/12/magento-add-radio-checkbox-button-to-admin-grid/"     class="crp_title">Magento add radio / checkbox button to admin grid</a></li><li><a href="http://ka.lpe.sh/2013/05/29/jquery-redirect-page-with-javascript-alternative/"     class="crp_title">jQuery redirect page, with javascript alternative</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-submitting-form-in-admin-redirects-to-dashboard/"     class="crp_title">Magento: Submitting form in admin redirects to dashboard</a></li><li><a href="http://ka.lpe.sh/2012/09/13/magento-get-product-attribute-select-option-idlabelvalue/"     class="crp_title">Magento: Get product attribute&#8217;s select option id/label/value</a></li><li><a href="http://ka.lpe.sh/2013/05/20/magento-pinterest-extension-plugin-autopin-multiple-product-images/"     class="crp_title">Magento Pinterest extension Auto Pin multiple product images Plugin</a></li></ul></div>'
categories:
    - jQuery
tags:
    - checkbox
    - jquery
---

![jQuery javascript framework](http://ka.lpe.sh/wp-content/uploads/2013/06/jquery-logo.png)Using jQuery, check whether checkbox is checked or not using 4 different ways in this post.

Below code relies on jQuery’s [is](http://api.jquery.com/is/ "jQuery is method") method to check if the checkbox is checked or not. If you want to lookup the checkbox by *class* instead of *id*, just replace *\#yourCheckboxID* with *.yourCheckboxClassName*

{{< highlight js "style=emacs" >}}if($(‘#yourCheckboxID’).is(‘:checked’)) {  
 //do whatever you want here, checkbox is checked  
} else {  
 //do whatever you want here, checkbox is NOT checked  
}{{< /highlight >}}

Other alternative to check same thing:  
{{< highlight js "style=emacs" >}}$(‘#yourCheckboxID’).change(function() {  
 if(this.checked) {  
 //checkbox is checked  
 } else {  
 //checkbox is NOT checked  
 }  
});{{< /highlight >}}  
Above code is the better way and my favorite. It will simply observe the checkbox and when it’s “changed”, the above function will get triggered. Once triggered, it will check the changed object’s (checkbox) attribute “checked”. If it finds the attribute is set, then returns true otherwise returns false.

Third way of doing it is:  
{{< highlight js "style=emacs" >}}if($(‘#yourCheckboxID’).attr(‘checked’) {  
 //checkbox is checked  
} else {  
 //checkbox is NOT checked  
}{{< /highlight >}}  
Above code will check the checkbox’s attribute “checked”, if present it will give true and if not present, it will give false.

Since jQuery 1.6, the new method has been introduced which is called [prop](http://api.jquery.com/prop/ "jQuery prop method"). If you are using jQuery 1.6 or above, you can use following code to check if checkbox is checked or not:  
{{< highlight js "style=emacs" >}}if($(‘#yourCheckboxID’).prop(‘checked’)) {  
 //checkbox is checked  
} else {  
 //checkbox is NOT checked  
}{{< /highlight >}}