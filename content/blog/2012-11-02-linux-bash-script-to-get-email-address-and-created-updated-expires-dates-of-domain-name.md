---
id: 386
title: 'Linux: Bash script to get email address and created/updated/expires dates of domain name'
date: '2012-11-02T07:43:38+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=386'
permalink: /index.php/2012/11/02/linux-bash-script-to-get-email-address-and-created-updated-expires-dates-of-domain-name/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/11/02/linux-bash-script-to-check-availability-of-domain-names-in-differnet-tlds/"     class="crp_title">Linux: Bash script to check availability of domain names in differnet TLDs</a></li><li><a href="http://ka.lpe.sh/2013/02/09/linux-magento-daily-useful-development-commands/"     class="crp_title">Linux/Magento: Daily useful development commands</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2013/04/25/magento-special-price-products-page/"     class="crp_title">Magento Special price products page</a></li><li><a href="http://ka.lpe.sh/2012/07/24/magento-add-customer-facebook-twitter-google-pinterest-handles/"     class="crp_title">Magento: Add customer Facebook, Twitter, Google+, Pinterest handles</a></li></ul></div>'
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
    - whois
---

In linux, to check the whois of any domain name, the simple command is:  
{{< highlight php "style=emacs" >}}whois domainname.com{{< /highlight >}}  
But, it will show you so many things which are not important, e.g. it will show you the NOTICE and TERMS of USE and so many other things.

If you are only concerned of getting the email address and creation/updation/expiry date of domain name from whois, here is the bash script that will help you out.  
First create a bash script file, e.g. whoisEmailAndDates.sh and give it permissions to run:  
{{< highlight php "style=emacs" >}}touch whoisEmailAndDates.sh  
chmod 744 whoisEmailAndDates.sh{{< /highlight >}}

Now, copy below code and paste it in the newly created file:  
{{< highlight perl "style=emacs" >}}#!/bin/sh

echo “”  
echo “######## WHOIS: “$1

\# Whois using the input variable  
whois $1 |\\

\# Remove EOL characters  
tr -d ‘\\015\\032’ |\\

\# Remove leading spaces  
sed ‘s/^ *//’ |\\

\# Remove common unnecessary words from output  
grep -v -e “http://” -e “WHOIS” > wtmp1.txt

\# Display all of the date lines and email addresses  
grep -Eio ‘([[:alnum:]_.]+@[[:alnum:]_]+ ?\\.[[:alpha:].]{2,6})’ wtmp1.txt  
egrep -i “ate: ” wtmp1.txt

\# Remove the tmp file  
rm -rf wtmp1.txt

echo “######## DONE!”  
echo “”{{< /highlight >}}

Now, run the script for the domain:  
{{< highlight php "style=emacs" >}}./whoisEmailAndDates.sh google.com{{< /highlight >}}  
You’ll be greeted with following output!  
{{< highlight perl "style=emacs" >}}######## WHOIS: google.com  
admin@google.com  
admin@google.com  
admin@google.com  
admin@google.com  
Updated Date: 20-jul-2011  
Creation Date: 15-sep-1997  
Expiration Date: 14-sep-2020  
\######## DONE!{{< /highlight >}}