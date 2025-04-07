---
id: 445
title: 'Magento: Create database backups daily programatically by cron'
date: '2013-02-02T20:18:58+00:00'
author: kalpesh
layout: post
tags:
    - Magento
tags:
    - 'magento daily backup cron'
    - 'magento database backup programatically'
    - 'magento replace old database backups'
---

It’s a good practice to create your database backup every day/week. But to manually go to Magento admin and create backup daily is a cumbersome process. You can’t guarantee that your database will be secure especially if you are on a cloud storage. Backups are MUST and if it’s automated, life becomes very easier.

This code will create backup of your Magento DB and place it to var/backups directory.  
{{< highlight php "style=emacs" >}}public function backup()  
{  
 try {

 $backupDb = Mage::getModel(‘backup/db’);  
 $backup = Mage::getModel(‘backup/backup’)  
 ->setTime(time())  
 ->setType(‘db’)  
 ->setPath(Mage::getBaseDir(“var”) . DS . “backups”);

 $backupDb->createBackup($backup);

 return Mage::helper(‘core’)->__(‘Backup successfully created’);

 } catch (Exception $e) {  
 Mage::logException($e);  
 }

 return $this;  
}{{< /highlight >}}  
  
Now, you can set the cron to run every midnight and call this above method to automatically create your DB backups. Sounds good? But there is a problem. As Magento DB size is huge, running daily/weekly backups will soon fill up your hardrives like hell.

So, we will now first create new DB database backup through our above method, and after it’s created we will delete the older backups just to free up the disk space.

{{< highlight php "style=emacs" >}}public function endsWith($haystack, $needle)  
{  
 $length = strlen($needle);  
 if ($length == 0) {  
 return true;  
 }

 return (substr($haystack, -$length) === $needle);  
}

public function backup()  
{

 //get all the older db backup files in an array  
 $filelist = array();  
 if ($handle = opendir(Mage::getBaseDir(‘var’) . DS . “backups” . DS)) {  
 while ($entry = readdir($handle)) {  
 if ($this->endsWith($entry, “_db.gz”)) {  
 $filelist[] = $entry;  
 }  
 }  
 closedir($handle);  
 }

 try {  
 //create the db backup  
 $backupDb = Mage::getModel(‘backup/db’);  
 $backup = Mage::getModel(‘backup/backup’)  
 ->setTime(time())  
 ->setType(‘db’)  
 ->setPath(Mage::getBaseDir(“var”) . DS . “backups”);

 $backupDb->createBackup($backup);

 //delete all older db backup files we found  
 foreach((array)$filelist as $fileToDelete) {  
 unlink(Mage::getBaseDir(“var”) . DS . “backups” . DS . $fileToDelete);  
 }

 return Mage::helper(‘core’)->__(‘Backup successfully created’);

 } catch (Exception $e) {  
 Mage::logException($e);  
 }

 return $this;  
}{{< /highlight >}}

Now you can set the CRON to run the file every midnight, which calls the above backup() method. You will now get daily fresh backups replacing the old ones 🙂

If you are not sure how to create a cron, check this link: http://www.magentocommerce.com/wiki/1_-_installation_and_configuration/how_to_setup_a_cron_job