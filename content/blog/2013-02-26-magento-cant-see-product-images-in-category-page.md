---
id: 496
title: 'Magento: Can&#8217;t see product images in category page'
date: '2013-02-26T17:15:50+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=496'
permalink: /index.php/2013/02/26/magento-cant-see-product-images-in-category-page/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/12/magento-image-resize-compression-reduces-quality-jpeg/"     class="crp_title">Magento: Image resize/compression reduces quality of JPEG</a></li><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2013/05/10/magento-get-products-by-attribute-set/"     class="crp_title">Magento get products by attribute set id or name</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
    - 'Magento frontend'
tags:
    - 'category page product images not showing'
    - 'magento product images does not show'
    - 'set product image small image thumbnail'
---

**Set product image as small image and thumbnail programatically**

If you see your images in product detail page but don’t see it in category page, it’s because your product have images (image attribute filled) but not *small_image* and *thumbnail* which are required to display on category page. If there are only few products you want to set small_image and thumbnail, then it’s easy to go to *Manage Products > Individual Product > Images tab > Set small image and thumbnail radio button*. But when it comes to hundreds/thousands of products, you better want it programatically way.

Make a file in your Magento root and place the below code in it. Then run that file and you have just copied your Product Image to small image and thumbnail as well!

{{< highlight php "style=emacs" >}}<?php ini_set('display_errors',1);
require 'app/Mage.php';
Mage::app();

$products = Mage::getModel('catalog/product')->
getCollection()->addAttributeToSelect(‘*’);  
foreach ($products as $product) {  
 if (!$product->hasImage()) continue;  
 if (!$product->hasSmallImage()) $product->setSmallImage($product->getImage());  
 if (!$product->hasThumbnail()) $product->setThumbnail($product->getImage());  
 $product->save();  
}  
echo ‘Finished!’;  
?>{{< /highlight >}}