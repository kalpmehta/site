---
id: 1069
title: '[Resolved] WordPress update error'
date: '2016-03-28T23:43:54+00:00'
author: kalpesh
layout: post
tags:
    - Wordpress
tags:
    - 'update error'
    - wordpress
---

If you are getting below (or any WordPress update) error when you are updating your WordPress to latest version, the problem could be:

***500 Internal Server Error***

 PHP Fatal error: Call to undefined function wp_oembed_add_host_js() in /var/www/production/blog/wp-admin/about.php on line 31

– **PHP version.** Make sure the PHP version you have meets the required PHP version of new WordPress update.  
– **Opcode cache.** If you are using opcode cache like APC, clear the cache.  
– **WordPress cache.** Flush the WordPress cache (Wordfence, WP Super Cache, W3 Total Cache, etc.) you are using.  
– **CloudFlare.** If you are using external cache like CloudFlare, make sure you also flush it if you still see the above error.

Refresh the update page and see if this resolves for you!