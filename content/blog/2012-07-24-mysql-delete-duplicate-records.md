---
id: 296
title: 'Mysql delete duplicate records leaving one'
date: '2012-07-24T17:22:49+00:00'
author: kalpesh
layout: post
tags:
    - MySQL
tags:
    - delete
    - 'duplicate records'
    - mysql
    - remove
---

Mysql delete duplicate records leaving one row. Consider that there are many duplicate records in the table and you want to remove it. Now, we can select it by applying GROUP BY but the question is how to delete all the duplicate records (of field some_id below) EXCEPT one that should be there. So, lets say I have following table with duplicate data as shown:  
**Tablename: test**  
{{< highlight sql "style=emacs" >}}   
unique_id | some_id  
——————–  
1 | 1  
2 | 1  
3 | 2  
4 | 2  
5 | 1  
{{< /highlight >}}  
  
Solution:  
{{< highlight sql "style=emacs" >}} DELETE t1 FROM test t1, test t2 WHERE t1.unique_id > t2.unique_id AND t1.some_id = t2.some_id;{{< /highlight >}}

Final Result:  
{{< highlight sql "style=emacs" >}}   
unique_id | some_id  
——————–  
1 | 1  
3 | 2  
{{< /highlight >}}