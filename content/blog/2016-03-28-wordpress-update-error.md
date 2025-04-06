---
id: 1069
title: '[Resolved] WordPress update error'
date: '2016-03-28T23:43:54+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1069'
permalink: /index.php/2016/03/28/wordpress-update-error/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/06/27/wordpress-plugin-install-without-ftp/"     class="crp_title">WordPress plugin install without FTP</a></li><li><a href="http://ka.lpe.sh/2013/10/20/magento-fatal-error-call-to-a-member-function-rewrite-on-a-non-object-in/"     class="crp_title">Magento Error: Fatal error: Call to a member function rewrite() on a non-object in&hellip;</a></li><li><a href="http://ka.lpe.sh/2013/05/22/magento-recoverable-error-argument-1-passed-to/"     class="crp_title">Magento Recoverable Error Argument 1 passed to Mage_Core_Model_Store::setWebsite() must be an instance of&hellip;</a></li><li><a href="http://ka.lpe.sh/2014/06/22/magento-clear-all-caches-from-command-line/"     class="crp_title">Magento: Clear all caches from command line</a></li><li><a href="http://ka.lpe.sh/2013/12/01/magento-redis-read-error-on-connection/"     class="crp_title">Magento Redis read error on connection</a></li></ul></div>'
categories:
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