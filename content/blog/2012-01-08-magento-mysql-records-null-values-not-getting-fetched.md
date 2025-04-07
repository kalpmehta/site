---
id: 179
title: 'Magento: Mysql records with NULL values are not fetched in query'
date: '2012-01-08T09:23:13+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - 'is null'
    - magento
    - 'magento orm'
    - 'query is null'
---

After banging my head on my desk trying to get the records with NULL values with Magento ORM, it was found that writing  
{{< highlight php "style=emacs" >}}$collection->addAttributeToFilter(‘somefield’, ‘null’)  
$collection->addAttributeToFilter(‘somefield’, array(‘is’ => ‘null’)){{< /highlight >}}  
will check for any blank values like this: *WHERE somefield = ”*

So if you want to fetch records that have NULL values in Magento style, you need to write as following:  
{{< highlight php "style=emacs" >}}$collection->addAttributeToFilter(‘somefield’, array(‘null’=>’null’){{< /highlight >}}  
will check like *WHERE somefield = null*

Hope this saves someone’s time!