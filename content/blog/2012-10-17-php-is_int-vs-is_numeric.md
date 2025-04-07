---
id: 353
title: 'PHP: is_int() vs is_numeric()'
date: '2012-10-17T14:53:07+00:00'
author: kalpesh
layout: post
tags:
    - PHP
tags:
    - 'php check variable integer'
    - 'php is_int vs is_numeric'
---

Both of the functions looks similar, but there is a difference, which can screw your time if you’re not aware of it and using blindly! is_int() seems same to is_numeric(), checking the variable if it’s integer or not, but it’s not exactly what you’re thinking.

The key difference between these two functions is that is_int() checks the **type** of variable, while is_numeric() checks the **value** of the variable.

From PHP.net,  
*is_int:* Find whether the type of a variable is integer  
*is_numeric:* Finds whether a variable is a number or a numeric string

So, if you check something like:  
{{< highlight php "style=emacs" >}}$var = “123”;{{< /highlight >}}  
$var is a string of numbers, not an integer value.  
Therefor *is_int should return false* as it’s not an integer, it’s a string.  
However it is a numeric string, so hence *is_numeric should return true*.