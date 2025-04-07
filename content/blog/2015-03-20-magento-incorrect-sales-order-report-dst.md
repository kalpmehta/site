---
id: 979
title: 'Magento bug: Incorrect sales order report during DST'
date: '2015-03-20T02:49:19+00:00'
author: kalpesh
layout: post

tags:
    - Magento
    - 'Magento admin'
tags:
    - bug
    - magento
    - 'sales order grid'
    - 'sales order report'
---

Before 6 months I found a bug in Magento CE 1.9 and EE 1.13 (latest versions at that time) in Sales Order report calculation during Daylight Savings Time period. I reported it to Magento through their Bug Tracking ticket but after 6 months also there is no reply no progress on that issue. I provided all the details on how to reproduce it and also provided solution to fix the issue. The issue is not yet resolved in latest Magento versions (I have checked Enterprise Edition 1.14.1.0 which is latest stable version now) so I decided to post it online so that other developers/clients who are experiencing same issue during DST (which have started) period can fix it and fetch correct numbers.

Ticket in Magento bug tracker (you would need to login to see):  
<http://www.magentocommerce.com/bug-tracking/issue/index/id/254>

**Overview of issue:**  
Sales order grid data (Admin->Sales->Orders) for certain date range is not matching with the report sales order data (Admin->Reports->Sales->Orders). There is some difference in numbers which made me drill into the Magento source code. Upon further investigation I saw Zend_Date’s set method was used without 2nd argument which took the date in wrong format messing with the totals.

**Steps to reproduce:**  
1\. Login in Admin panel  
2\. Go to Reports->Sales->Orders screen  
3\. Filter orders for some date range which should fall in Daylight savings time.  
4\. Notice the totals which are shown are not 100% correct.

**Expected Result:**  
The totals in Reports->Sales->Orders screen should match totals in Sales->Orders grid screen when downloading CSV from there. I have attached the issue in detail along with solution in the attached file.

**Actual Result:**  
The totals in Reports->Sales->Orders screen is not coming correct when date range filter falls in daylight savings time.

**Magento version affected:**  
It seems all CE and EE versions, I only checked CE 1.8, 1.9 and EE 1.13, 1.14

**Files Affected:**  
app/code/core/Mage/Reports/Model/Resource/Report/Abstract.php  
app/code/core/Mage/Reports/Model/Mysql4/Report/Abstract.php (In older magento versions using Mysql4 instead of Resource)

**Technical Details:**  
 In the file app/code/core/Mage/Reports/Model/Resource/Report/Abstract.php  
function: _getTZOffsetTransitions  
line 418, $dateTimeObject->set($tr[‘time’]);

$dateTimeObject is object of Zend_Date() and expects parameter 2 for the date/time format  
<http://framework.zend.com/manual/1.11/en/zend.date.basic.html#zend.date.simple.functions.set>

After changing this line:  
{{< highlight http >}} $dateTimeObject->set($tr[‘time’]);{{< /highlight >}}  
with  
{{< highlight http >}} $dateTimeObject->set($tr[‘time’], Varien_Date::DATETIME_INTERNAL_FORMAT);{{< /highlight >}}

the issue was fixed and the order totals were shown correctly in Reports->Sales->Order screen.

**Important Note:** After the above change it is required to re-build lifetime statistics of Orders to update database table sales_order_aggregated_created.

Make the change by copying the core file to your local so that future upgrade will not overwrite your fix.