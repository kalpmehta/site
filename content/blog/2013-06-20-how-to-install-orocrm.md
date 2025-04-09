---
id: 732
title: 'OroCRM Installation guide'
date: '2013-06-20T00:43:02+00:00'
author: kalpesh
layout: post
tags:
    - Linux
    - OroCRM
tags:
    - orocrm
---

I will show you here how to install OroCRM in your machine. OroCRM is the latest open-source CRM tool developed by MageCore. It’s little difficult to make it work on your system as there are some issues which occurs in installing it, and there is also no thorough documentation as of now. It’s in pre-alpha release and just publicly available since 3 weeks. I will show you how to install OroCRM assuming you have Linux system.

**Requirements**: Symfony 2, Doctrine 2, PHP >= 5.3.3

![OroCRM login - installation guide](http://ka.lpe.sh/uploads/2013/06/orocrm-login.png)

– Clone the CRM application Git repository in your local. It should be done in your web server’s root directory (e.g. /var/www/).  
{{< highlight http >}} git clone http://gitlab.orocrm.com/crm-application.git{{< /highlight >}}  
  
– Now switch to the newly created crm-application directory and make the parameters.yml file with your configuration changes.  
{{< highlight http >}} cd crm-application  
cp app/config/parameters.dist.yml app/config/parameters.yml  
vi app/config/parameters.yml{{< /highlight >}}

– Edit composer.json, add symfony/assestic-bundle to prevent future error:

*PHP Fatal error: Class ‘Assetic\\Util\\PathUtils’ not found in /var/www/crm-application/vendor/symfony/assetic-bundle/Symfony/Bundle/AsseticBundle/Command/DumpCommand.php on line 216*

{{< highlight http >}} replace:  
“require”: {  
 “php”: “>=5.3.3”,  
 “oro/platform”: “dev-master”,  
 “oro/crm”: “dev-master”  
 },{{< /highlight >}}  
with  
{{< highlight http >}} ”require”: {  
 “php”: “>=5.3.3”,  
 “oro/platform”: “dev-master”,  
 “oro/crm”: “dev-master”,  
 “symfony/assetic-bundle”: “2.3.*@dev”  
 },{{< /highlight >}}

– This will install composer. If you already have it, just ignore this step.  
{{< highlight http >}} curl -s https://getcomposer.org/installer | php{{< /highlight >}}

– This will install all the things which are listed in composer.json file and necessary by Oro; like zendframework, doctrine, twig, symfony, monolog, oro, etc..  
{{< highlight http >}} php composer.phar install –prefer-dist{{< /highlight >}}

Change permissions of cache and logs directory to world-writeable. Otherwise you will get errors like:

*PHP Fatal error: Uncaught exception ‘RuntimeException’ with message ‘Unable to write in the logs directory (/var/www/crm-application/app/logs)\\n’ in …  
PHP Fatal error: Uncaught exception ‘RuntimeException’ with message ‘Unable to create the cache directory (/var/www/crm-application/app/cache/prod)\\n’ in …*

{{< highlight http >}} chmod -R 777 app/cache  
chmod -R 777 app/logs  
or, find app/cache app/logs -type d -exec chmod 777 {} +{{< /highlight >}}

– Finally, run the install bash script  
{{< highlight http >}} ./install.sh{{< /highlight >}}

You should now able to see the login screen of OroCRM if everything went good. If you face any error, check below errors and how to solve it.

*Login credentials are:*  
username: admin  
password: admin

—————-

*Fatal error: Class ‘Assetic\\Util\\PathUtils’ not found in /var/www/crm-application/vendor/symfony/assetic-bundle/Symfony/Bundle/AsseticBundle/Command/DumpCommand.php on line 216*

edit composer.json, replace:  
{{< highlight http >}} ”require”: {  
 “php”: “>=5.3.3”,  
 “oro/platform”: “dev-master”,  
 “oro/crm”: “dev-master”  
 },{{< /highlight >}}  
with  
{{< highlight http >}} ”require”: {  
 “php”: “>=5.3.3”,  
 “oro/platform”: “dev-master”,  
 “oro/crm”: “dev-master”,  
 “symfony/assetic-bundle”: “2.3.*@dev”  
 },{{< /highlight >}}

and run

{{< highlight http >}} php composer.phar upate –prefer-dist  
./install.sh{{< /highlight >}}

—————-

Are you missing JS and CSS files? Skinless? Run below two commands.  
{{< highlight http >}} php composer.phar upate –prefer-dist  
php app/console assetic:dump{{< /highlight >}}

*It will output:*  
Dumping all dev assets.  
Debug mode is off.

04:55:49 [dir+] /var/www/crm-application/app/../web/css  
04:55:49 [file+] /var/www/crm-application/app/../web/css/oro.all.css  
04:55:55 [file+] /var/www/crm-application/app/../web/css/oro.css  
04:55:59 [file+] /var/www/crm-application/app/../web/js/oro.all.js  
04:56:54 [file+] /var/www/crm-application/app/../web/css/oro.user.css  
04:56:57 [file+] /var/www/crm-application/app/../web/js/oro.user.js  
04:57:00 [file+] /var/www/crm-application/app/../web/js/oro.user.show.js  
04:57:01 [file+] /var/www/crm-application/app/../web/js/orocrm.account.account.js  
04:57:02 [file+] /var/www/crm-application/app/../web/js/orocrm.contact.js  
04:57:03 [file+] /var/www/crm-application/app/../web/js/oroapp.all.js  
04:57:09 [file+] /var/www/crm-application/app/../web/css/oro.crm.css

—————-

After login, are you seeing the below message?

*ERROR:  
Translator.locale = ‘en’;  
Translator.defaultDomains = [“messages”];  
Translator.add(“validators:You must select at least {{ limit }} role”, “You must select at least {{ limit }} role.|You must select at least {{ limit }} roles.”);*

Just remove “i18n/validators/en” from the URL and submit the base URL. You should see the OroCRM Dashboard.

—————

Create apache virtualhost at */etc/apache2/sites-available/orocrm* to access OroCRM by *http://dev.orocrm.local/* from your browser.  
Notice the document root is web directory.

{{< highlight http >}} <virtualhost>  
 ServerAdmin webmaster@localhost  
 ServerName dev.orocrm.local</virtualhost>

 DocumentRoot /var/www/crm-application/web  
 <directory></directory>  
 Options Indexes FollowSymLinks MultiViews  
 AllowOverride All  
 Order allow,deny  
 allow from all

 ErrorLog ${APACHE_LOG_DIR}/error.log  
 LogLevel warn  
 CustomLog ${APACHE_LOG_DIR}/access.log combined  
{{< /highlight >}}

enable the site and reload web server  
{{< highlight http >}} a2ensite orocrm  
service apache2 reload{{< /highlight >}}

add entry to hosts file  
*vi /etc/hosts*  
and add  
{{< highlight http >}} 127.0.0.1 dev.orocrm.local{{< /highlight >}}