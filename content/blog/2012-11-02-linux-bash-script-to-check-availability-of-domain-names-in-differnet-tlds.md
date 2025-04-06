---
id: 392
title: 'Linux: Bash script to check availability of domain names in differnet TLDs'
date: '2012-11-02T08:00:57+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=392'
permalink: /index.php/2012/11/02/linux-bash-script-to-check-availability-of-domain-names-in-differnet-tlds/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-get-email-address-and-created-updated-expires-dates-of-domain-name/"     class="crp_title">Linux: Bash script to get email address and created/updated/expires dates of domain name</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2011/06/14/magento-get-file-paths-and-urls/"     class="crp_title">Magento get file paths and URLs</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-check-if-any-particular-customer-is-currently-logged-in/"     class="crp_title">Magento: Check if any particular customer is currently logged in</a></li></ul></div>'
snapEdIT:
    - '1'
snapFB:
    - 's:166:"a:1:{i:0;a:4:{s:4:"doFB";s:1:"1";s:8:"PostType";s:1:"A";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:56:"New post (%TITLE%) has been published on %SITENAME% blog";}}";'
snapLI:
    - 's:178:"a:1:{i:0;a:4:{s:4:"doLI";s:1:"1";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:46:"New post has been published on %SITENAME% blog";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";}}";'
snapTW:
    - 's:99:"a:1:{i:0;a:3:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"0";}}";'
categories:
    - 'Domain name'
    - Linux
tags:
    - 'domain name'
    - linux
    - script
---

If you want to check whether your desired domain name is available or not in different extensions, it’s tiresome to search it for each and every tld. There are also limits of performing query to whois on websites, where they will not allow you unlimited whois information queries. It’s better to have your own script which will tell you the availibility of domain name in different extensions, right from your terminal.

Below script will check your domain name for TLDs .com, .net, .org, .info, .us, .co, .tel, .tv, .biz, .cc, .ru, .eu, .in, .it, .sk, .com.au, .sh, .re and .dk  
But you can add other TLDs also if you want.

First create a file, e.g. chkWhois.sh, and give it proper permission to execute.  
{{< highlight php "style=emacs" >}}touch chkWhois.sh  
chmod 744 chkWhois.sh{{< /highlight >}}

Now, copy below code to this newly created file  
  
{{< highlight perl "style=emacs" >}}#!/bin/bash

if [ “$#” == “0” ]; then  
 echo “You need to supply at least one domain name!”  
 exit 1  
fi

DOMAINS=( ‘.com’ ‘.net’ ‘.info’ ‘.us’ ‘.co’ \\  
‘.org’ ‘.tel’ ‘.biz’ ‘.tv’ ‘.cc’ ‘.eu’ ‘.ru’ \\  
‘.in’ ‘.it’ ‘.sk’ ‘.com.au’ ‘.sh’ ‘.re’ ‘.dk’ )

ELEMENTS=${#DOMAINS[@]}

while (( “$#” )); do

 for (( i=0;i<$ELEMENTS;i++)); do whois $1${DOMAINS[${i}]} | egrep -q '^No match|^NOT FOUND|^Not fo|AVAILABLE|^No Data Fou|has not been regi|No entri' if [ $? -eq 0 ]; then echo "$1${DOMAINS[${i}]} : available" fi done shift done{{< /highlight >}} Run this for your desired name to check, {{< highlight php "style=emacs" >}}./chkWhois.sh kalpesh{{< /highlight >}} You'll get output will all the TLD's your name is available for! {{< highlight php "style=emacs" >}}kalpesh.us : available kalpesh.tel : available kalpesh.cc : available kalpesh.eu : available kalpesh.ru : available kalpesh.sk : available kalpesh.sh : available kalpesh.re : available kalpesh.dk : available{{< /highlight >}} Have fun!