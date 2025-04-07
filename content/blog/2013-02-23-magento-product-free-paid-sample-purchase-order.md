---
id: 484
title: 'Magento: Product Free/Paid SAMPLE Purchase Order'
date: '2013-02-23T08:41:44+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento frontend'
tags:
    - 'magento sample product purchase'
    - 'order sample of product'
---

If you want to allow your customers to order for sample of any product, before purchasing the actual product, it becomes very tough as in a product page you can’t have two products (sample + full) allowed. But it’s not a good idea to display sample products as Individually, it makes sense only in the actual product page just near the Add To Cart button.

![Magento Sample product purchase](http://ka.lpe.sh/wp-content/uploads/2013/02/magento-sample-purchase.png)

But the question is, how to have TWO SKUs in a single product detail page? Here is the code that will do exactly what you want now. Open your catalog/product/view.phtml template file and put this code just below the code “$this->getChildHtml(‘addtocart’);”

{{< highlight php "style=emacs" >}}<button http:="" onclick="window.location.href='/order_sample.php?sku=<?php echo $this->htmlEscape($_product->getSku()) ?>'” title=”Request Sample for <?php echo $this->htmlEscape($_product->getName()) ?>” class=”button btn-cart” ><span><span>Order Sample – $1</span></span></button>{{< /highlight >}}<br />
\<!--more--><br />
And then create a php file “order_sample.php” in the root of your Magento installation:</p>
<p>{{< highlight php "style=emacs" >}}require_once ‘app/Mage.php’;<br />
Mage::app();</p>
<p>$sku = $_GET[‘sku’];<br />
if(!$sku)<br />
{<br />
        header(“Location: “.Mage::getStoreConfig(‘web/unsecure/base_url’));<br />
        exit;<br />
}<br />
$prod = Mage::getModel(‘catalog/product’);<br />
$p = $prod->loadByAttribute(‘sku’,$sku);</p>
<p>//validate if we have that SKU before creating it\’s sample..<br />
if(!is_object($p) || strstr($sku, ‘S-‘))<br />
{<br />
        header(“Location: “.Mage::getStoreConfig(‘web/unsecure/base_url’));<br />
        exit;<br />
}<br />
$name = $p->getName();</p>
<p>//check if you already have the Sample product, then don\’t create new..<br />
$p = $prod->loadByAttribute(‘sku’,’S-‘.$sku);<br />
if(is_object($p))<br />
        $pId = $p->getId();<br />
else<br />
        $pId = false;</p>
<p>if(!$pId) {</p>
<p>$product = $prod;<br />
$product->setSku(‘S-‘.$sku); //Prepending “S-” before original SKU to prevent misunderstanding<br />
$product->setName(“Sample of “.$name);<br />
$product->setDescription(“Sample of “.$name);<br />
$product->setShortDescription($name.” – Sample”);<br />
$product->setPrice(1.00); //Price always $1<br />
$product->setTypeId(‘simple’);<br />
$product->setAttributeSetId(4); // default – CHECK YOUR VALUE<br />
$product->setCategoryIds(“0”); // CHECK YOUR VALUE(s)<br />
$product->setWeight(0.000);<br />
$product->setTaxClassId(0); // none<br />
$product->setVisibility(1); // not visible individually<br />
$product->setStatus(1); // enabled</p>
<p>// assign product to the default website..<br />
$product->setWebsiteIds(array(Mage::app()->getStore(true)->getWebsite()->getId()));</p>
<p>// get product\’s general info such price, status, description..<br />
$stockData = $product->getStockData();</p>
<p>// update stock data using new data..<br />
$stockData[‘qty’] = 1; //we’re not managing stock anyhow<br />
$stockData[‘is_in_stock’] = 1;<br />
$stockData[‘manage_stock’] = 0; //don’t manage sample stocks<br />
$stockData[‘max_sale_qty’] = 1; //sample can’t be purchased more than 1 qty</p>
<p>$product->setStockData($stockData);</p>
<p>$product->save();<br />
$pId = $product->getId();<br />
}</p>
<p>//redirect and add to cart page..<br />
header(“Location: /checkout/cart/add/product/”.$pId.”/”);<br />
exit;{{< /highlight >}}</p>
<p>Inspired from: <a href=" style="float:left;padding-left:5px;" type="button">http://opensourcetalking.com/magento/magento-free-samples-solution.html</button>