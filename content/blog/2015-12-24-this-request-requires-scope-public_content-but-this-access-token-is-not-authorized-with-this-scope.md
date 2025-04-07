---
id: 1051
title: '[SOLVED] This request requires scope=public_content, but this access token is not authorized with this scope'
date: '2015-12-24T00:59:02+00:00'
author: kalpesh
layout: post
tags:
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