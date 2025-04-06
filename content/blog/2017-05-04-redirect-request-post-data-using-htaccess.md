---
id: 1101
title: 'Redirect request with POST data using .htaccess'
date: '2017-05-04T21:34:37+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=1101'
permalink: /index.php/2017/05/04/redirect-request-post-data-using-htaccess/
s4_url2s:
    - ''
s4_image2s:
    - ''
s4_ctitle:
    - ''
s4_cdes:
    - ''
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2015/12/24/this-request-requires-scope-public_content-but-this-access-token-is-not-authorized-with-this-scope/"     class="crp_title">[SOLVED] This request requires scope=public_content, but this access token is not authorized with this scope</a></li><li><a href="http://ka.lpe.sh/2015/09/04/magento-zipcode-4-tax-calculation-bug-fix/"     class="crp_title">Magento: Zipcode + 4 tax calculation bug fix</a></li><li><a href="http://ka.lpe.sh/2014/11/07/magento-error-scp-404-get-sppajax___siducoid460pid123/"     class="crp_title">Magento error: SCP 404: GET /spp/ajax/?___SID=Uco/?id=460&#038;pid=123</a></li><li><a href="http://ka.lpe.sh/2014/10/07/magento-code-already-exists-fix/"     class="crp_title">Magento fix for error &#8220;Code already exists.&#8221;</a></li><li><a href="http://ka.lpe.sh/2016/02/16/magento-2-events-observer-list/"     class="crp_title">Magento 2 events observer list</a></li></ul></div>'
categories:
    - Apache
    - htaccess
tags:
    - '307 status code'
    - data
    - htaccess
    - post
    - redirect
---

By default, if you want to redirect request with POST data, browser redirects it via GET with 302 redirect. This also drops all the POST data associated with the request. Browser does this as a precaution to prevent any unintentional re-submitting of POST transaction.

But what if you want to redirect anyway POST request with it’s data? In HTTP 1.1, there is a status code for this. Status code 307 indicates that the request should be repeated with the same HTTP method and data. So your POST request will be repeated along with it’s data if you use this status code.

From https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html,  
*If the 307 status code is received in response to a request other than GET or HEAD, **the user agent MUST NOT automatically redirect the request** unless it can be confirmed by the user, since this might change the conditions under which the request was issued.*

I did this in one of the website to redirect HTTP request to HTTPS for a specific page.

{{< highlight http >}} RewriteEngine on  
RewriteCond %{SERVER_PORT} !443  
RewriteCond %{REQUEST_URI} string_to_match_in_url  
RewriteCond %{REQUEST_METHOD} POST  
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [L,R=307]{{< /highlight >}}

For this to work, you need to have mod_rewrite enabled on the server. The first RewriteCond checks if the request is NOT coming as HTTPS, otherwise it will go in endless loop. If yes, the second RewriteCond checks if the URL contains a string we are looking for. Then if that URL is being submitted as POST method. If everything matches, then we redirect the request using HTTPS secure protocol retaining the POST method and the associated data.