---
id: 335
title: 'Ubuntu: Delete temporary/cache files'
date: '2012-10-10T21:13:27+00:00'
author: kalpesh
layout: post
tags:
    - Linux
tags:
    - 'clean ubuntu'
    - 'delete cache files'
    - 'ubuntu remove temporary files'
---

It’s necessary to clean unnecessary files from your operating system and free up space. In Ubuntu, this is very easy if you have admin privileges.

Below command will remove all the unnecessary package files, which are no longer used by their packages. You can say they are orphaned files, not needed anymore.  
**sudo apt-get autoremove**

Below command will remove all the cache and unnecessary files from your system. It will delete everything and make your system clean from temporary files and orphaned files.  
**sudo apt-get clean**