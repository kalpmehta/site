---
id: 946
title: 'Magento fix for error "Code already exists."'
date: '2014-10-07T23:09:09+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
    - 'Magento error'
tags:
    - error
    - magento
    - 'magento admin'
    - tax
---

Fix for Magento error **Code already exists.** in Sales > Tax > Manage Tax Rules, when saving the rule.

When trying to save Tax rules in Magento, you may get “Code already exists.” error if there are lots of tax rates passing in POST. Magento error is not making sense here, as the issue is something different. Basically when you post the data in PHP, it limits maximum post variables which should pass to the server. For me, that limit was 1000 in max_input_vars, which by changing to 20000 solved this issue and Magento successfully accepted my changes without any error.

To change max_input_vars to higher value, you need to edit in PHP.ini file for max_input_vars like this:  
{{< highlight http >}} max_input_vars 20000{{< /highlight >}}

But as editing PHP.ini requires restarting apache to reflect the changes, I did the change in .htaccess file just for Tax rule modification and later reverted it.

You can edit .htaccess to make this change by copy-pasting below line at the end of the file:  
{{< highlight http >}} php_value max_input_vars 20000{{< /highlight >}}

Now you should be able to change Tax rules even if you have lots of tax rates posting through for that change! I prefered to revert .htaccess back to what it was as I didn’t need to change tax rules frequently.

Note: If the above does not solve the issue for you, make sure your Tax Rule name is not duplicating with another tax rule name.