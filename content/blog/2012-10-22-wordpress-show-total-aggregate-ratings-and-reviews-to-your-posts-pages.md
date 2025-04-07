---
id: 364
title: 'WordPress: Show total/aggregate ratings and reviews to your posts/pages'
date: '2012-10-22T15:07:22+00:00'
author: kalpesh
layout: post
tags:
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