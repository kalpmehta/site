---
id: 1051
title: '[SOLVED] This request requires scope=public_content, but this access token is not authorized with this scope'
date: '2015-12-24T00:59:02+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1051'
permalink: /index.php/2015/12/24/this-request-requires-scope-public_content-but-this-access-token-is-not-authorized-with-this-scope/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2015/03/28/magento-2-security-bug/"     class="crp_title">Magento 2 &#8211; Security Bug in Customer Address section (Resolved)</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li><li><a href="http://ka.lpe.sh/2013/11/03/magento-remove-session-id-from-url/"     class="crp_title">Magento remove session id from URL</a></li><li><a href="http://ka.lpe.sh/2015/03/28/magento-checkout-cart-500-error/"     class="crp_title">Magento bug &#8211; Checkout cart 500 error &#8211; Redirect loops</a></li><li><a href="http://ka.lpe.sh/2014/10/07/magento-code-already-exists-fix/"     class="crp_title">Magento fix for error &#8220;Code already exists.&#8221;</a></li></ul></div>'
categories:
    - 'Instagram API'
tags:
    - instagram
---

***This request requires scope=public_content, but this access token is not authorized with this scope. The user must re-authorize your application with scope=public_content to be granted this permissions***

If you are getting this error while using Instagram API in Sandbox mode, all you need to do is authorize the scope by going to the below URL. Don’t forget to replace YOUR-CLIENT-ID with your Instagram client ID and YOUR-REDIRECT-URI with your valid redirect URI.

[https://api.instagram.com/oauth/authorize/?client_id=YOUR-CLIENT-ID&amp;redirect_uri=YOUR-REDIRECT-URI&amp;response_type=code&amp;scope=public_content](https://api.instagram.com/oauth/authorize/?client_id=YOUR-CLIENT-ID&redirect_uri=YOUR-REDIRECT-URI&response_type=code&scope=public_content)

You may also need to authorize **basic**, **comments**, **follower_list**, **likes** or/and **relationships** if you are getting any of the below errors.

***This request requires scope=comments, but this access token is not authorized with this scope. The user must re-authorize your application with scope=comments to be granted this permissions***

***This request requires scope=follower_list, but this access token is not authorized with this scope. The user must re-authorize your application with scope=follower_list to be granted this permissions***

***This request requires scope=likes, but this access token is not authorized with this scope. The user must re-authorize your application with scope=likes to be granted this permissions***

***This request requires scope=relationships, but this access token is not authorized with this scope. The user must re-authorize your application with scope=relationships to be granted this permissions***

To authorize ALL the above scopes at once use below link replacing your client ID and redirect URI:

[https://api.instagram.com/oauth/authorize/?client_id=YOUR-CLIENT-ID&amp;redirect_uri=YOUR-REDIRECT-URI&amp;response_type=code&amp;scope=basic+comments+follower_list+likes+relationships+public_content](https://api.instagram.com/oauth/authorize/?client_id=YOUR-CLIENT-ID&redirect_uri=YOUR-REDIRECT-URI&response_type=code&scope=basic+comments+follower_list+likes+relationships+public_content)