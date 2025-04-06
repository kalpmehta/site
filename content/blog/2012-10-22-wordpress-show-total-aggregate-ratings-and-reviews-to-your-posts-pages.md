---
id: 364
title: 'WordPress: Show total/aggregate ratings and reviews to your posts/pages'
date: '2012-10-22T15:07:22+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=364'
permalink: /index.php/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/18/magento-get-most-popular-products-in-a-category/"     class="crp_title">Magento Get most popular products in a category</a></li><li><a href="http://ka.lpe.sh/2012/02/12/magento-show-track-your-order-in-frontend-my-orders/"     class="crp_title">Magento: Show &#8220;track your order&#8221; in frontend &#8211; My Orders</a></li><li><a href="http://ka.lpe.sh/2013/02/23/magento-product-free-paid-sample-purchase-order/"     class="crp_title">Magento: Product Free/Paid SAMPLE Purchase Order</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-some-important-functions/"     class="crp_title">Magento: Some important functions</a></li><li><a href="http://ka.lpe.sh/2011/06/19/magento-checking-customer-admin-is-logged-in-or-not/"     class="crp_title">Magento: Checking customer/admin is logged in or not</a></li></ul></div>'
categories:
    - Wordpress
tags:
    - 'aggregate ratings reviews wordpress'
    - 'wordpress show total ratings'
    - 'wp customer reviews total aggregate ratings reviews'
---

After struggling for finding the way to show aggregate ratings and total number of reviews for the wordpress plugin WP Customer Reviews, I wrote it myself by studying their code. There has been several requests for this feature in their support page and around but they didn’t seem to be interested or didn’t got enough time to wrote this.

Okay, so for all the people who have been struggling to get total and/or aggregate number of ratings and reviews, here is the code that can work on any page/post.  
{{< highlight php "style=emacs" >}}global $wpdb;  
$pId = $post->ID; //if using in another page, use the ID of the post/page you want to show ratings for.  
$row = $wpdb->get_results(“SELECT COUNT(*) AS `total`,AVG(review_rating) AS `aggregate_rating`,MAX(review_rating) AS `max_rating` FROM wp_wpcreviews WHERE `page_id`= $pId AND `status`=1”);  
$max_rating = $row[0]->max_rating;  
$aggregate_rating = $row[0]->aggregate_rating;  
$total_reviews = $row[0]->total;  
$totl = $aggregate_rating * 20;  
$wpdb->flush();{{< /highlight >}}  
  
To show aggregate ratings in star form, simply add this:  
{{< highlight html "style=emacs" >}}

<div class="sp_rating" id="wpcr_respond_1"><div class="base"><div style="width: <?php echo $totl;?>%” class=”average”></div>
</div>
<p><?php echo ' ' . $total_reviews;?> Reviews</div>
<p>{{< /highlight >}}<br />
<em>Note: In the above code, please check the formatting of PHP tags, sometimes it’s just not formatted proper and as a result there will be wrong ratings displayed.</em></p>
<p>For displaying it as,<br />
Overall: 4.67 stars for 60 reviews.<br />
{{< highlight php "style=emacs" >}}echo “Overall: ” . $aggregate_rating . ” stars for ” . $total_reviews . ” reviews.”;{{< /highlight >}}</p>
"></div></div></div>