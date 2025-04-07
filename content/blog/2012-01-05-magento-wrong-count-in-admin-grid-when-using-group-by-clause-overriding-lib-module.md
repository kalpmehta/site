---
id: 168
title: 'Magento: Wrong count in admin Grid when using GROUP BY clause, overriding lib module'
date: '2012-01-05T09:47:31+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento admin'
tags:
    - 'magento admin'
    - 'magento getsize error'
    - 'overriding lib module'
    - 'wrong count in grid'
    - 'wrong record count'
---

If you have noticed or not, in version 1.5 of Magento when you use GROUP BY clause in any Grid.php file in admin, the count always display wrong. Many times it displays 1 even if there are hundreds of records. Due to this your pagination also doesn’t work. This is a bug in Magento. Your getSize() always returns wrong count whereas total records in grid are proper.

To fix this, you need to edit one of your core file. As it’s not a good practice to edit core file, we will here override the core file.  
Overriding LIB module

Copy Db.php file from magento / lib / Varien / Data / Collection / Db.php  
Paste it to your local directory so the resultant folder structure would look like this:  
magento / app / code / local / Varien / Data / Collection / Db.php  
  
Now open this file to edit and replace getSelectCountSql function with below one  
{{< highlight php "style=emacs" >}} public function getSelectCountSql()  
 {  
 $this->_renderFilters();

 $countSelect = clone $this->getSelect();  
 $countSelect->reset(Zend_Db_Select::ORDER);  
 $countSelect->reset(Zend_Db_Select::LIMIT_COUNT);  
 $countSelect->reset(Zend_Db_Select::LIMIT_OFFSET);  
 $countSelect->reset(Zend_Db_Select::COLUMNS);

 if(count($this->getSelect()->getPart(Zend_Db_Select::GROUP)) > 0) {  
 $countSelect->reset(Zend_Db_Select::GROUP);  
 $countSelect->distinct(true);  
 $group = $this->getSelect()->getPart(Zend_Db_Select::GROUP);  
 $countSelect->columns(“COUNT(DISTINCT “.implode(“, “, $group).”)”);  
 } else {  
 $countSelect->columns(‘COUNT(*)’);  
 }  
 return $countSelect;  
 }{{< /highlight >}}

*Updated the method for generic use*