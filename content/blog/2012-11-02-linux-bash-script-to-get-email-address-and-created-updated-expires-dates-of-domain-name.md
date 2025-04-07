---
id: 386
title: 'Linux: Bash script to get email address and created/updated/expires dates of domain name'
date: '2012-11-02T07:43:38+00:00'
author: kalpesh
layout: post
tags:
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