---
id: 1081
title: 'Magento: Multiple security vulnerabilities in Aheadworks Follow up Email extension'
date: '2016-11-17T20:46:55+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - Security
---

***IMPORTANT: If you are using this extension in any of the Magento store, please patch or upgrade it immediately if you have not done it yet. You can find more details on the affected versions and patches here:***  
<https://blog.aheadworks.com/2016/10/security-issue-follow-up-email-vulnerability/>  
<https://blog.aheadworks.com/2016/10/follow-email-security-patch/>

While modifying Aheadworks follow up extension on our store to meet our specific requirements, I discovered multiple security vulnerabilities in the extension. As the vulnerabilities were pretty serious, I immediately sent my discoveries to Magento team which they promptly sent to Aheadworks team. Aheadworks was quick enough to fix the vulnerabilities and rolled out the patches.

Link of the extension in Magento Marketplace:  
<https://marketplace.magento.com/aheadworks-follow-up-email.html>  
It allows store owners to send automated emails to customers who had abandoned their cart.  
![Aheadworks follow up email extension](http://ka.lpe.sh/uploads/2016/11/fue-2.png)

All the below vulnerabilities were found in the extension.

**1. SQL injection**  
**2. Directory Traversal vulnerability**  
*Attacker can traverse to any directory on the server. In earlier PHP versions (prior to 5.3.4), attacker can read any file on server including /etc/passwd*  
**3. Unrestricted Directories creation**  
*Attacker can create any number of directories and subdirectories with their desired name wherever web server has permissions*

I will not disclose any technical details and PoC of the vulnerabilties here to prevent wild exploits on Magento websites having this extension installed.

**Timeline:**  
Oct 6, 2016 – Discovered the SQL injection vulnerability  
Oct 6, 2016 – Emailed the vulnerability to Magento security and marketplace team  
Oct 7, 2016 – Emailed the vulnerability to Magento team  
Oct 7, 2016 – Magento forwarded my discoveries to Aheadworks team  
Oct 11, 2016 – Aheadworks released new version 3.6.6 and patch for older versions of the extension  
Oct 25, 2016 – Found further vulnerabilities on the same controller action, this time Directory Traversal and Unrestricted Directories creation vulnerabilities  
Oct 25, 2016 – Emailed the details to Magento team, they promptly notified to Aheadworks team  
Oct 27, 2016 – Fixed the vulnerabilities in new version 3.6.7 and released the patch for older versions