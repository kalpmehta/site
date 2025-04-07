---
id: 995
title: 'Magento 2 Security Bug in Customer Address section (Resolved)'
date: '2015-03-28T06:31:02+00:00'
author: kalpesh
layout: post


tags:
    - Magento2
tags:
    - bug
    - magento2
    - security
---

Magento 2 had a serious security bug where a website user can view and edit any customer’s address very easily. I reported this issue to Magento 2 team and they quickly fixed it and rolled it out in new beta version. All the beta versions up to **0.42.0-beta11** were affected, and from **0.74.0-beta1** it is fixed (I have not tested it yet).

Details about the bug and progress: <https://github.com/magento/magento2/issues/1107>

If you are using the affected Magento 2 versions for online demo or development please upgrade it. Though people use fake address in Demo stores, it is likely that some of them could have used their real address and details which can be accessible by anyone who knows about this bug.