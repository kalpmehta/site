---
id: 452
title: 'Linux/Magento: Daily useful development commands'
date: '2013-02-09T08:11:08+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=452'
permalink: /index.php/2013/02/09/linux-magento-daily-useful-development-commands/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/01/08/mysql-root-password-reset/"     class="crp_title">Mysql root password reset or create</a></li><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2012/10/10/ubuntu-delete-temporary-cache-files/"     class="crp_title">Ubuntu: Delete temporary/cache files</a></li><li><a href="http://ka.lpe.sh/2012/07/21/migrate-magento-to-new-server-domain-database-host/"     class="crp_title">Migrate magento to new server / domain / database / host</a></li><li><a href="http://ka.lpe.sh/2012/10/17/php-is_int-vs-is_numeric/"     class="crp_title">PHP: is_int() vs is_numeric()</a></li></ul></div>'
categories:
    - Linux
    - Magento
tags:
    - 'magento linux daily useful commands'
    - 'magento linux development commands'
    - 'routine important information'
---

These are the daily commands I use at work. This will definately help someone who is not familiar with all these commands in Linux and Magento.

**Linux: Search / Replace recursively**

find /path/here/ -type f -exec sed -i ‘s/search string/replace string/g’ {} \\;

**Linux: Find all files matching a string**

grep -r “string to search” /path/to/search/

Linux: In vi editor, copy/paste/delete/replace/insert/save/undo/redo/search-replace/goto  
Open file: vi filename  
Copy: yy (yank) (for multiple lines copy, 5yy – for copying 5 lines)  
Paste: p  
Delete: dd (for multiple lines delete, 5dd – for deleting 5 lines)  
Replace: r (on character you wish to replace, press r and enter new character)  
Insert: i or insert key  
Save: escape and : x (without space between : and x) (x = write and quit, w = write, q = quit, q! = quit without saving)  
Undo: u  
Redo: Ctrl+R  
Search: escape key THEN / THEN write string to find THEN enter  
Search-Replace: :%s/search string/replacement string/g  
Goto Line number: escape key THEN : THEN line number (e.g. :22 to go to 22nd line of current file)

**Linux: Search previous execute command in terminal**

in terminal, press Ctrl+R and type few characters.  
This will show you previous command matching that sequence of characters  
To check another command matching same characters, press Ctrl+R again

**Linux: Recursively change files/directories permissions**

find . -type d -exec chmod 0755 {} \\;  
find . -type f -exec chmod 0644 {} \\;

owner / read (4) + write (2) + execute (1)  
group / read (4) + write (2) + execute (1)  
world / read (4) + write (2) + execute (1)

**Linux: Show unique values of any column in CSV**

cat file.csv | cut -f 1 -d , | sort|uniq -c | tee tempfile

here, 1 = 1st column, which can be changed to view any column  
uniq -c = unique values with count of occurences of each value. You can omit -c to just see the unique values  
file.csv = filename, you can have any file here with any extension  
, = delimiter used to separate columns  
tee tempfile = moves the output to file “tempfile”

**Linux: Recursively change ownership of directories/files**

chown -R www-data:www-data magento  
-R = for recursive  
www-data:www-data = change owner to www-data (apache)  
magento = directory to change permission for, recursively

**Linux: Remove all Magento cache files**

From your magento root in terminal, execute this:  
rm -rf var/cache/*  
DON’T put any space after cache/ and *, otherwise it will delete your WHOLE magento project 😀

To delete all the active sessions on your magento store,  
rm -rf var/session/*  
  
**Linux: Download any Magento Extension through terminal**

./mage config-set preferred_state stable  
./mage clear-cache  
./mage sync  
./mage download community extension_name_here

for beta state, change “stable” to “beta” in the first command

**Linux: Start/Stop/Status/Restart Mysql, Apache2**

service apache2 start OR /etc/init.d/apache2 start  
service mysql start OR /etc/init.d/mysql start

replace start with stop, status, restart for respective operations

**Linux: To forcefully kill stubborn/hanged process**

In terminal, type “top” (without quotes)  
That will display all the processes running, just note down the process id to kill  
Then press key “k” and enter process id. Press enter key twice.

**Linux: Return to active terminal after remote server ssh is dead/not responding/session expired**

Press following keys to get back from remote server not responding (expired session)  
Enter ~ .

**Magento: Get all the methods of the class object**

Mage::log(get_class_methods(get_class($obj)));

**Magento: Testing Magento code/functionality**

Create a file in Magento root, test.php  
Copy this code inside it:  
<?php require_once('app/Mage.php');
	umask(0);
	Mage::app();

	// Magento code to test run here...
??>
  
Now run the script at http://magentoproject/test.php