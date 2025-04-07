---
id: 324
title: 'Magento: Submitting form in admin redirects to dashboard'
date: '2012-09-13T09:16:15+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'form redirects dashboard'
    - 'magento form post'
    - 'magento form redirection'
---

When trying to submit a form which is created in admin, it redirects to dashboard no matter how much you try. I faced this problem and tried many things but without any luck. Everything was running, for file upload I had enctype=”multipart/form-data” in form, checked the form action through firebug and run it directly in browser URL which was also going good. After so much frustration, googled the problem and found that I was not the only one to face this problem.

Finally, got one forum where I found the solution to this problem. In Magento, when submitting the form, you need to have one extra hidden field, with name “form_key” which should have form’s key value from session. Here is the line of code, which helped me in posting form successfully.

{{< highlight php "style=emacs" >}}<input name="form_key" type="hidden" value="<?php echo Mage::getSingleton('core/session')->getFormKey() ?>” /> {{< /highlight >}}</p>
<p>Hope this helps some frustrated mind 🙂</p>
"></input>