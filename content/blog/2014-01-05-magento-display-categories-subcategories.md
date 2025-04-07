---
id: 861
title: 'Magento display categories and sub-categories'
date: '2014-01-05T14:40:21+00:00'
author: kalpesh
layout: post
tags:
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