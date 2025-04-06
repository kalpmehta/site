---
id: 324
title: 'Magento: Submitting form in admin redirects to dashboard'
date: '2012-09-13T09:16:15+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=324'
permalink: /index.php/2012/09/13/magento-submitting-form-in-admin-redirects-to-dashboard/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/07/12/magento-add-radio-checkbox-button-to-admin-grid/"     class="crp_title">Magento add radio / checkbox button to admin grid</a></li><li><a href="http://ka.lpe.sh/2012/11/02/buy-pinterest-autopost-images-right-from-your-website/"     class="crp_title">Buy: Pinterest AutoPost images right from your website!</a></li><li><a href="http://ka.lpe.sh/2011/06/05/magento-1-5-cant-login-to-admin-panel-after-fresh-install/"     class="crp_title">Magento 1.5: Cannot login to admin panel after fresh install</a></li><li><a href="http://ka.lpe.sh/2012/07/19/magento-interview-questions-and-answers/"     class="crp_title">Magento Interview questions and answers</a></li><li><a href="http://ka.lpe.sh/2011/07/09/magento-cant-loginadd-items-in-chrome-and-ie/"     class="crp_title">Magento: Can&#8217;t login/add items in Chrome and IE</a></li></ul></div>'
categories:
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