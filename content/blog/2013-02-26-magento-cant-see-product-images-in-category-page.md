---
id: 496
title: 'Magento: Can&#8217;t see product images in category page'
date: '2013-02-26T17:15:50+00:00'
author: kalpesh
layout: post
tags:
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