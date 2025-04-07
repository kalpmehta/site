---
id: 392
title: 'Linux: Bash script to check availability of domain names in differnet TLDs'
date: '2012-11-02T08:00:57+00:00'
author: kalpesh
layout: post
tags:
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