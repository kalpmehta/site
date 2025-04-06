---
id: 861
title: 'Magento display categories and sub-categories'
date: '2014-01-05T14:40:21+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=861'
permalink: /index.php/2014/01/05/magento-display-categories-subcategories/
snapEdIT:
    - '1'
snapFB:
    - 's:162:"a:1:{i:0;a:4:{s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";s:4:"doFB";i:0;}}";'
snapLI:
    - 's:174:"a:1:{i:0;a:4:{s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:4:"doLI";i:0;}}";'
snapTW:
    - 's:95:"a:1:{i:0;a:3:{s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";s:4:"doTW";i:0;}}";'
snap_isAutoPosted:
    - '1'
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/"     class="crp_title">WordPress: Show total/aggregate ratings and reviews to your posts/pages</a></li><li><a href="http://ka.lpe.sh/2013/06/03/prototype-utility-methods/"     class="crp_title">Prototype Utility Methods &#8211; Commonly used prototypejs functions</a></li><li><a href="http://ka.lpe.sh/2013/05/26/magento-get-subcategories-of-a-category/"     class="crp_title">Magento get subcategories of a category by category ID</a></li><li><a href="http://ka.lpe.sh/2013/07/21/magento-get-all-categories-of-a-product/"     class="crp_title">Magento get all categories of a product</a></li><li><a href="http://ka.lpe.sh/2013/06/01/return-false-vs-preventdefault-javascript/"     class="crp_title">return false vs preventDefault in javascript</a></li></ul></div>'
categories:
    - Magento
    - 'Magento frontend'
tags:
    - category
    - magento
    - subcategory
---

Magento display categories and sub-categories. Below code will show all the parent and child categories along with show/hide functionalities by jQuery.

{{< highlight http >}} 

<div class="block block-layered-nav"><div class="block-title"> **<span><?php echo $this->
__(‘Shop By Category’) ?></span>** </div><div class="block-content"> <?php $productid = Mage::registry('current_product')->
getId();  
 $product = Mage::getSingleton(‘catalog/product’)->load($productid);  
 $parentIds = $product->getCategoryIds();  
 $parentId = $parentIds[0];  
 $_categories = Mage::getBlockSingleton(‘catalog/navigation’);  
 foreach ($_categories->getStoreCategories() as $_category) {  
 $category = Mage::getModel(‘catalog/category’);  
 $category->load($_category->getId());  
 $subcategories = explode(‘,’, $category->getChildren());  
 if(!in_array($_category->getId(),$parentIds)) { $hide=”display:none”; $inactive=”inactive”; } else { $hide=””; $inactive=”active”; }  
 ?> <div style="padding:5px 5px 0px 10px"><div child="" class="cat parent <?php echo $inactive;?>” style=”font-size:15px”><?php echo $_category->getName() ?></div>
<div class=" style="<?php echo $hide;?>“><br />
                         <?php foreach ($subcategories as $subcategoryId) {
                                $category->load($subcategoryId);<br />
                                if($category->getChildren() == ”) {<br />
                                        if(in_array($subcategoryId,$parentIds)) { $bold = “font-weight:bold”; } else { $bold = “”; }<br />
                                      echo ‘</p>
<div class=" subcat="">[<div class="parent active"><?php echo $category->
getName() ?></div><div class="child"> <?php $subsubcategories = explode(',', $category->
getChildren());  
 foreach($subsubcategories as $subsubcatid) {  
 if(in_array($subsubcatid, $parentIds)) { $bold = “font-weight:bold”; } else { $bold = “”; }  
 $category->load($subsubcatid);  
 echo ‘ <div style="padding-left:10px;'.$bold.'">[ jQuery('.block-content .cat').click(function(){ var t = jQuery(this); if(jQuery(this).next().css('display')=='none') { jQuery('.col-left .block-content .child').hide(); t.next().show(); t.next().find('div.child').show("slow"); } else { t.next().hide(); t.next().find('div.child').hide("slow"); } }); {{< /highlight >}} ](<' . $category->getURL() . ‘”>’ . $category->getName() . ‘</a></div>
<p>‘;<br />
                                        } ?>
                                        </p></div>
</p></div>
<p>                        <?php }
                        }
                        ?>
                        </div>
</p></div>
<p>                <?php

        } ?>
    </div>
</div>
<p><script type=>)</div></div>](<' . $category->getURL() . ‘”>’ . $category->getName() . ‘</a></div>
<p>‘;<br />
                                 } else {?></p>
<div class=>)</div></div></div></div>