---
id: 1117
title: 'Setting up Magento 2.2.3 on Valet+ (requires MacOS)'
date: '2018-03-20T00:15:28+00:00'
author: kalpesh
layout: post
tags:
    - Magento2
tags:
    - magento2
    - valet+
---

Wondering what is Valet+? It is a development environment for MacOS. If you have previously used Vagrant and/or Docker, I think you would just love Valet+. Valet+ is very easy yet fast development environment, as it doesn’t require you to edit /etc/hosts, vhosts, mysql, etc.. For more information on Valet+ and how it differs with Valet, please read this: <https://github.com/weprovide/valet-plus/blob/master/readme.md>

Let me know in comments section which one you prefer out of these 3?

Okay so let’s come to topic and start preparing to install Valet and Magento.

**1.) Install [Homebrew](https://brew.sh/) if you do not have it already on your Mac**

**2.) Let’s install PHP 7.1**

brew install homebrew/php/php71

If you already have php70, you can unlink it before running above command:

brew unlink php70

{{< highlight http >}} 

Kalpeshs-MBP:~ kalpesh$ brew install php71  
Updating Homebrew…  
==> Installing php71 from homebrew/php  
==> Installing dependencies for homebrew/php/php71: libpng, freetype, gettext, icu4c, jpeg, libtool, unixodbc, readline  
==> Installing homebrew/php/php71 dependency: libpng  
==> Downloading https://downloads.sourceforge.net/libpng/libpng-1.6.34.tar.xz  
==> Downloading from https://downloads.sourceforge.net/project/libpng/libpng16/1.6.34/libpng-1.6.34.tar.xz  
\######################################################################## 100.0%  
==> ./configure –disable-silent-rules –prefix=/usr/local/Cellar/libpng/1.6.34  
==> make  
==> make test  
==> make install  
🍺 /usr/local/Cellar/libpng/1.6.34: 26 files, 1.2MB, built in 2 minutes 22 seconds  
==> Installing homebrew/php/php71 dependency: freetype  
==> Downloading https://downloads.sourceforge.net/project/freetype/freetype2/2.9/freetype-2.9.tar.bz2  
==> Downloading from https://svwh.dl.sourceforge.net/project/freetype/freetype2/2.9/freetype-2.9.tar.bz2  
\######################################################################## 100.0%  
==> ./configure –prefix=/usr/local/Cellar/freetype/2.9 –without-harfbuzz  
==> make  
==> make install  
🍺 /usr/local/Cellar/freetype/2.9: 60 files, 2.7MB, built in 1 minute 53 seconds  
==> Installing homebrew/php/php71 dependency: gettext  
==> Downloading https://homebrew.bintray.com/bottles/gettext-0.19.8.1.yosemite.bottle.tar.gz  
\######################################################################## 100.0%  
==> Pouring gettext-0.19.8.1.yosemite.bottle.tar.gz  
==> Caveats  
This formula is keg-only, which means it was not symlinked into /usr/local,  
because macOS provides the BSD gettext library &amp; some software gets confused if both are in the library path.

If you need to have this software first in your PATH run:  
echo ‘export PATH=”/usr/local/opt/gettext/bin:$PATH”‘ >> ~/.bash_profile

For compilers to find this software you may need to set:  
LDFLAGS: -L/usr/local/opt/gettext/lib  
CPPFLAGS: -I/usr/local/opt/gettext/include

==> Summary  
🍺 /usr/local/Cellar/gettext/0.19.8.1: 1,934 files, 17.0MB  
==> Installing homebrew/php/php71 dependency: icu4c  
==> Downloading https://ssl.icu-project.org/files/icu4c/60.2/icu4c-60_2-src.tgz  
\######################################################################## 100.0%  
==> ./configure –prefix=/usr/local/Cellar/icu4c/60.2 –disable-samples –disable-tests –enable-static –with-library-bits=64  
==> make  
==> make install  
==> Caveats  
This formula is keg-only, which means it was not symlinked into /usr/local,  
because macOS provides libicucore.dylib (but nothing else).

If you need to have this software first in your PATH run:  
echo ‘export PATH=”/usr/local/opt/icu4c/bin:$PATH”‘ >> ~/.bash_profile  
echo ‘export PATH=”/usr/local/opt/icu4c/sbin:$PATH”‘ >> ~/.bash_profile

For compilers to find this software you may need to set:  
LDFLAGS: -L/usr/local/opt/icu4c/lib  
CPPFLAGS: -I/usr/local/opt/icu4c/include  
For pkg-config to find this software you may need to set:  
PKG_CONFIG_PATH: /usr/local/opt/icu4c/lib/pkgconfig

==> Summary  
🍺 /usr/local/Cellar/icu4c/60.2: 249 files, 67.2MB, built in 9 minutes 15 seconds  
==> Installing homebrew/php/php71 dependency: jpeg  
==> Downloading http://www.ijg.org/files/jpegsrc.v9c.tar.gz  
\######################################################################## 100.0%  
==> ./configure –disable-silent-rules –prefix=/usr/local/Cellar/jpeg/9c  
==> make install  
🍺 /usr/local/Cellar/jpeg/9c: 21 files, 736.3KB, built in 1 minute 30 seconds  
==> Installing homebrew/php/php71 dependency: libtool  
==> Downloading https://homebrew.bintray.com/bottles/libtool-2.4.6_1.yosemite.bottle.tar.gz  
\######################################################################## 100.0%  
==> Pouring libtool-2.4.6_1.yosemite.bottle.tar.gz  
==> Caveats  
In order to prevent conflicts with Apple’s own libtool we have prepended a “g”  
so, you have instead: glibtool and glibtoolize.  
==> Summary  
🍺 /usr/local/Cellar/libtool/2.4.6_1: 70 files, 3.7MB  
==> Installing homebrew/php/php71 dependency: unixodbc  
==> Downloading http://www.unixodbc.org/unixODBC-2.3.5.tar.gz  
\######################################################################## 100.0%  
==> ./configure –prefix=/usr/local/Cellar/unixodbc/2.3.5_1 –sysconfdir=/usr/local/etc –enable-static –enable-gui=no  
==> make install  
🍺 /usr/local/Cellar/unixodbc/2.3.5_1: 41 files, 1.9MB, built in 4 minutes 22 seconds  
==> Installing homebrew/php/php71 dependency: readline  
==> Downloading https://homebrew.bintray.com/bottles/readline-7.0.3_1.yosemite.bottle.tar.gz  
\######################################################################## 100.0%  
==> Pouring readline-7.0.3_1.yosemite.bottle.tar.gz  
==> Caveats  
This formula is keg-only, which means it was not symlinked into /usr/local,  
because macOS provides the BSD libedit library, which shadows libreadline.  
In order to prevent conflicts when programs look for libreadline we are  
defaulting this GNU Readline installation to keg-only..

For compilers to find this software you may need to set:  
LDFLAGS: -L/usr/local/opt/readline/lib  
CPPFLAGS: -I/usr/local/opt/readline/include

==> Summary  
🍺 /usr/local/Cellar/readline/7.0.3_1: 46 files, 1.5MB  
==> Installing homebrew/php/php71  
==> Downloading https://php.net/get/php-7.1.14.tar.bz2/from/this/mirror  
==> Downloading from https://secure.php.net/get/php-7.1.14.tar.bz2/from/this/mirror  
\######################################################################## 100.0%  
==> ./configure –prefix=/usr/local/Cellar/php71/7.1.14_25 –localstatedir=/usr/local/var –sysconfdir=/usr/local/etc/php/7.1 –with-config-file-path=/usr/local/etc/php/7  
==> make  
==> make install  
==> Caveats  
The php.ini file can be found in:  
/usr/local/etc/php/7.1/php.ini

✩✩✩✩ Extensions ✩✩✩✩

If you are having issues with custom extension compiling, ensure that you are using the brew version, by placing /usr/local/bin before /usr/sbin in your PATH:

PATH=”/usr/local/bin:$PATH”

PHP71 Extensions will always be compiled against this PHP. Please install them using –without-homebrew-php to enable compiling against system PHP.

✩✩✩✩ PHP CLI ✩✩✩✩

If you wish to swap the PHP you use on the command line, you should add the following to ~/.bashrc, ~/.zshrc, ~/.profile or your shell’s equivalent configuration file:  
export PATH=”$(brew –prefix homebrew/php/php71)/bin:$PATH”

✩✩✩✩ FPM ✩✩✩✩

To launch php-fpm on startup:  
mkdir -p ~/Library/LaunchAgents  
cp /usr/local/opt/php71/homebrew.mxcl.php71.plist ~/Library/LaunchAgents/  
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php71.plist

The control script is located at /usr/local/opt/php71/sbin/php71-fpm

OS X 10.8 and newer come with php-fpm pre-installed, to ensure you are using the brew version you need to make sure /usr/local/sbin is before /usr/sbin in your PATH:

PATH=”/usr/local/sbin:$PATH”

You may also need to edit the plist to use the correct “UserName”.

Please note that the plist was called ‘homebrew-php.josegonzalez.php71.plist’ in old versions of this formula.

With the release of macOS Sierra the Apache module is now not built by default. If you want to build it on your system you have to install php with the –with-httpd option. See brew options php71 for more details.

By 31st March 2018 we will deprecate and archive the PHP tap.  
Some of the formulae will be migrated to homebrew-core.

For more details, see https://github.com/Homebrew/homebrew-php/issues/4721

To have launchd start homebrew/php/php71 now and restart at login:  
brew services start homebrew/php/php71  
==> Summary  
🍺 /usr/local/Cellar/php71/7.1.14_25: 345 files, 39.9MB, built in 11 minutes 5 seconds

{{< /highlight >}}

3.) Install Composer

brew install homebrew/php/composer

4.) Finally install Valet+

composer global require weprovide/valet-plus

{{< highlight http >}} Kalpeshs-MBP:valet kalpesh$ composer global require weprovide/valet-plus  
Changed current directory to /Users/kalpesh/.composer  
Using version ^1.0 for weprovide/valet-plus  
./composer.json has been created  
Loading composer repositories with package information  
Updating dependencies (including require-dev)  
Package operations: 15 installs, 0 updates, 0 removals  
– Installing tightenco/collect (v5.4.33): Downloading (100%)  
– Installing symfony/process (v3.4.6): Downloading (100%)  
– Installing nategood/httpful (0.2.20): Downloading (100%)  
– Installing psr/container (1.0.0): Downloading (100%)  
– Installing container-interop/container-interop (1.2.0): Downloading (100%)  
– Installing php-di/invoker (1.3.3): Downloading (100%)  
– Installing psr/log (1.0.2): Downloading (100%)  
– Installing symfony/debug (v4.0.6): Downloading (100%)  
– Installing symfony/polyfill-mbstring (v1.7.0): Downloading (100%)  
– Installing symfony/console (v3.4.6): Downloading (100%)  
– Installing mnapoli/silly (1.5.1): Downloading (100%)  
– Installing psr/simple-cache (1.0.1): Downloading (100%)  
– Installing illuminate/contracts (v5.6.12): Downloading (100%)  
– Installing illuminate/container (v5.6.12): Downloading (100%)  
– Installing weprovide/valet-plus (1.0.11): Downloading (100%)  
symfony/console suggests installing symfony/event-dispatcher ()  
symfony/console suggests installing symfony/lock ()  
Writing lock file  
Generating autoload files{{< /highlight >}}

5.) Add export PATH in your .bash_profile

vi ~/.bash_profile

and add below line on top (after PATH line if you have one already)

export PATH=”$PATH:$HOME/.composer/vendor/bin”

to reflect our current changes in the current terminal tab session, run:

source ~/.bash_profile

6.) Now let’s run the command

valet install

{{< highlight http >}} 

[nginx] Stopping

[php71] Stopping

[mysql] Stopping

[redis] Stopping

[devtools] Installing

[wp-cli] Installing

[n98-magerun] Installing

Updating Homebrew…

[n98-magerun2] Installing

Updating Homebrew…

==> Auto-updated Homebrew!

Updated 1 tap (caskroom/cask).

No changes to formulae.

[pv] Installing

Updating Homebrew…

[php71] Installing extensions

[php71-apcu] Installing

[php71-intl] Installing

[php71-mcrypt] Installing

Updating Homebrew…

[php71-opcache] Installing

[php71-geoip] Installing

Updating Homebrew…

[php71] Restarting

[dnsmasq] Restarting

[mysql] Installing

[mysql-utilities] Installing

[mysql] Stopping

[mysql] Configuring

[mysql] Restarting

[redis] Installing

[redis] Restarting

[mailhog] Installing

[mailhog] Restarting

[nginx] Restarting

Valet installed successfully!

{{< /highlight >}}

Now if you ping any domain with tld .test, it should respond:

ping magento.test

{{< highlight http >}} Kalpeshs-MBP:valet kalpesh$ ping magento.test  
PING magento.test (127.0.0.1): 56 data bytes  
64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.059 ms  
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.082 ms  
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.099 ms{{< /highlight >}}

7.) Create sites folder to install Magento inside it

mkdir sites

cd sites

8.) Run below command to serve our Magento site

valet park

9.) Let’s install Magento 2.2.2 now (At this time there was no 2.2.3 in magerun2. But don’t worry we will upgrade it to 2.2.3 later)

magerun2 install

{{< highlight http >}} 

Kalpeshs-MBP:mage2 kalpesh$ magerun2 install

Magento 2 Installation

[1] magento-ce-2.2.2  
[2] magento-ce-2.2.1  
[3] magento-ce-2.2.0  
[4] magento-ce-2.1.11  
[5] magento-ce-2.1.10  
[6] magento-ce-2.1.9  
[7] magento-ce-2.1.8  
[8] magento-ce-2.1.7  
[9] magento-ce-2.1.6  
[10] magento-ce-2.1.5  
[11] magento-ce-2.1.4  
[12] magento-ce-2.1.3  
[13] magento-ce-2.1.2  
[14] magento-ce-2.1.1  
[15] magento-ce-2.1.0  
[16] magento-ce-2.0.16  
[17] magento-ce-2.0.15  
[18] magento-ce-2.0.14  
[19] magento-ce-2.0.13  
[20] magento-ce-2.0.12  
[21] magento-ce-2.0.11  
[22] magento-ce-2.0.10  
[23] magento-ce-2.0.9  
[24] magento-ce-2.0.8  
[25] magento-ce-2.0.7  
[26] magento-ce-2.0.6  
[27] magento-ce-2.0.5  
[28] magento-ce-2.0.4  
[29] magento-ce-2.0.2  
[30] magento-ce-2.0.1  
[31] magento-ce-2.0.0  
Choose a magento version: 1  
Enter installation folder: [./magento]./magento  
Found executable composer.phar  
Installing magento/project-community-edition (2.2.2)  
– Installing magento/project-community-edition (2.2.2)  
Downloading: 100%

Created project in /Users/kalpesh/sites/magento  
Loading composer repositories with package information  
Updating dependencies  
– Installing magento/magento-composer-installer (0.1.13)  
Downloading: 100%

– Installing magento/zendframework1 (1.13.1)  
Downloading: 100%

– Installing zendframework/zend-stdlib (2.7.7)  
Downloading: 100%

– Installing zendframework/zend-hydrator (1.1.0)  
Downloading: 100%

– Installing psr/container (1.0.0)  
Loading from cache

– Installing container-interop/container-interop (1.2.0)  
Loading from cache

– Installing zendframework/zend-validator (2.10.2)  
Downloading: 100%

– Installing zendframework/zend-escaper (2.5.2)  
Downloading: 100%

– Installing zendframework/zend-uri (2.5.2)  
Downloading: 100%

– Installing zendframework/zend-loader (2.5.1)  
Downloading: 100%

– Installing zendframework/zend-http (2.7.0)  
Downloading: 100%

– Installing psr/log (1.0.2)  
Loading from cache

– Installing monolog/monolog (1.23.0)  
Downloading: 100%

– Installing psr/http-message (1.0.1)  
Downloading: 100%

– Installing zendframework/zend-diactoros (1.7.1)  
Downloading: 100%

– Installing zendframework/zend-psr7bridge (0.2.2)  
Downloading: 100%

– Installing zendframework/zend-servicemanager (2.7.10)  
Downloading: 100%

– Installing zendframework/zend-filter (2.7.2)  
Downloading: 100%

– Installing zendframework/zend-inputfilter (2.8.1)  
Downloading: 100%

– Installing zendframework/zend-form (2.11.0)  
Downloading: 100%

– Installing zendframework/zend-eventmanager (2.6.4)  
Downloading: 100%

– Installing zendframework/zend-mvc (2.7.13)  
Downloading: 100%

– Installing zendframework/zend-math (2.7.0)  
Downloading: 100%

– Installing zendframework/zend-crypt (2.6.0)  
Downloading: 100%

– Installing zendframework/zend-code (3.1.0)  
Downloading: 100%

– Installing symfony/polyfill-mbstring (v1.7.0)  
Loading from cache

– Installing symfony/debug (v3.0.9)  
Downloading: 100%

– Installing symfony/console (v2.8.36)  
Downloading: 100%

– Installing oyejorge/less.php (v1.7.0.14)  
Downloading: 100%

– Installing symfony/process (v2.8.36)  
Downloading: 100%

– Installing symfony/finder (v3.4.6)  
Downloading: 100%

– Installing symfony/filesystem (v3.4.6)  
Downloading: 100%

– Installing seld/phar-utils (1.0.1)  
Downloading: 100%

– Installing seld/jsonlint (1.7.1)  
Downloading: 100%

– Installing seld/cli-prompt (1.0.3)  
Downloading: 100%

– Installing justinrainbow/json-schema (5.2.7)  
Downloading: 100%

– Installing composer/spdx-licenses (1.3.0)  
Downloading: 100%

– Installing composer/semver (1.4.2)  
Downloading: 100%

– Installing composer/ca-bundle (1.1.0)  
Downloading: 100%

– Installing composer/composer (1.4.1)  
Downloading: 100%

– Installing colinmollenhour/credis (1.8.2)  
Downloading: 100%

– Installing colinmollenhour/php-redis-session-abstract (v1.3.4)  
Downloading: 100%

– Installing tedivm/jshrink (v1.2.0)  
Downloading: 100%

– Installing magento/framework (101.0.2)  
Downloading: 100%

– Installing magento/module-deploy (100.2.2)  
Downloading: 100%

– Installing magento/module-config (101.0.2)  
Downloading: 100%

– Installing magento/module-media-storage (100.2.0)  
Downloading: 100%

– Installing magento/module-require-js (100.2.0)  
Downloading: 100%

– Installing magento/module-store (100.2.2)  
Downloading: 100%

– Installing magento/module-user (101.0.1)  
Downloading: 100%

– Installing magento/module-email (100.2.1)  
Downloading: 100%

– Installing magento/module-ui (101.0.2)  
Downloading: 100%

– Installing magento/module-translation (100.2.2)  
Downloading: 100%

– Installing magento/module-developer (100.2.1)  
Downloading: 100%

– Installing magento/module-backend (100.2.2)  
Downloading: 100%

– Installing magento/module-authorization (100.2.0)  
Downloading: 100%

– Installing magento/module-quote (101.0.2)  
Downloading: 100%

– Installing magento/module-catalog-inventory (100.2.2)  
Downloading: 100%

– Installing magento/module-page-cache (100.2.1)  
Downloading: 100%

– Installing magento/module-url-rewrite (101.0.2)  
Downloading: 100%

– Installing magento/module-cms-url-rewrite (100.2.0)  
Downloading: 100%

– Installing magento/module-variable (100.2.1)  
Downloading: 100%

– Installing magento/module-catalog (102.0.2)  
Downloading: 100%

– Installing magento/module-catalog-url-rewrite (100.2.2)  
Downloading: 100%

– Installing magento/module-eav (101.0.1)  
Downloading: 100%

– Installing magento/module-import-export (100.2.2)  
Downloading: 100%

– Installing magento/module-security (100.2.0)  
Downloading: 100%

– Installing magento/module-customer (101.0.2)  
Downloading: 100%

– Installing magento/module-integration (100.2.1)  
Downloading: 100%

– Installing magento/module-widget (101.0.1)  
Downloading: 100%

– Installing magento/module-cms (102.0.2)  
Downloading: 100%

– Installing magento/module-theme (100.2.2)  
Downloading: 100%

– Installing magento/module-rule (100.2.0)  
Downloading: 100%

– Installing magento/module-catalog-rule (101.0.2)  
Downloading: 100%

– Installing magento/module-sales-rule (101.0.1)  
Downloading: 100%

– Installing magento/module-reports (100.2.2)  
Downloading: 100%

– Installing magento/module-gift-message (100.2.0)  
Downloading: 100%

– Installing magento/module-directory (100.2.1)  
Downloading: 100%

– Installing magento/module-tax (100.2.2)  
Downloading: 100%

– Installing magento/module-sales (101.0.2)  
Downloading: 100%

– Installing magento/module-shipping (100.2.2)  
Downloading: 100%

– Installing magento/module-msrp (100.2.0)  
Downloading: 100%

– Installing magento/module-payment (100.2.1)  
Downloading: 100%

– Installing magento/module-checkout (100.2.2)  
Downloading: 100%

– Installing magento/module-contact (100.2.1)  
Downloading: 100%

– Installing magento/module-rss (100.2.0)  
Downloading: 100%

– Installing magento/module-wishlist (101.0.1)  
Downloading: 100%

– Installing magento/module-sales-sequence (100.2.0)  
Downloading: 100%

– Installing magento/module-grouped-product (100.2.1)  
Downloading: 100%

– Installing magento/module-downloadable (100.2.1)  
Downloading: 100%

– Installing magento/module-newsletter (100.2.1)  
Downloading: 100%

– Installing magento/module-review (100.2.2)  
Downloading: 100%

– Installing magento/module-catalog-import-export (100.2.2)  
Downloading: 100%

– Installing magento/module-product-alert (100.2.0)  
Downloading: 100%

– Installing magento/module-indexer (100.2.1)  
Downloading: 100%

– Installing magento/module-cron (100.2.1)  
Downloading: 100%

– Installing magento/module-backup (100.2.1)  
Downloading: 100%

– Installing temando/module-shipping-m2 (1.0.4)  
Downloading: 100%

– Installing dotmailer/dotmailer-magento2-extension (2.3.8)  
Downloading: 100%

– Installing shopialfb/facebook-module (2.2.1)  
Downloading: 100%

– Installing magento/language-zh_hans_cn (100.2.0)  
Downloading: 100%

– Installing magento/language-pt_br (100.2.0)  
Downloading: 100%

– Installing magento/language-nl_nl (100.2.0)  
Downloading: 100%

– Installing magento/language-fr_fr (100.2.0)  
Downloading: 100%

– Installing magento/language-es_es (100.2.0)  
Downloading: 100%

– Installing magento/language-en_us (100.2.0)  
Downloading: 100%

– Installing magento/language-de_de (100.2.0)  
Downloading: 100%

– Installing magento/theme-frontend-blank (100.2.1)  
Downloading: 100%

– Installing magento/theme-frontend-luma (100.2.2)  
Downloading: 100%

– Installing magento/theme-adminhtml-backend (100.2.1)  
Downloading: 100%

– Installing magento/module-wishlist-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-weee (100.2.0)  
Downloading: 100%

– Installing magento/module-webapi (100.2.1)  
Downloading: 100%

– Installing magento/module-webapi-security (100.2.0)  
Downloading: 100%

– Installing magento/module-version (100.2.0)  
Downloading: 100%

– Installing magento/module-vault (101.0.1)  
Downloading: 100%

– Installing magento/module-usps (100.2.0)  
Downloading: 100%

– Installing magento/module-ups (100.2.1)  
Downloading: 100%

– Installing magento/module-tax-import-export (100.2.0)  
Downloading: 100%

– Installing magento/module-swatches-layered-navigation (100.2.0)  
Downloading: 100%

– Installing magento/module-configurable-product (100.2.2)  
Downloading: 100%

– Installing magento/module-swatches (100.2.1)  
Downloading: 100%

– Installing magento/module-swagger (100.2.1)  
Downloading: 100%

– Installing magento/module-robots (100.2.0)  
Downloading: 100%

– Installing magento/module-sitemap (100.2.2)  
Downloading: 100%

– Installing magento/module-signifyd (100.2.1)  
Downloading: 100%

– Installing magento/module-send-friend (100.2.0)  
Downloading: 100%

– Installing magento/module-search (100.2.2)  
Downloading: 100%

– Installing magento/module-catalog-search (100.2.2)  
Downloading: 100%

– Installing magento/module-sample-data (100.2.1)  
Downloading: 100%

– Installing magento/module-sales-inventory (100.2.0)  
Downloading: 100%

– Installing magento/module-sales-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-review-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-release-notification (100.2.0)  
Downloading: 100%

– Installing magento/module-quote-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-product-video (100.2.1)  
Downloading: 100%

– Installing magento/module-persistent (100.2.0)  
Downloading: 100%

– Installing magento/module-instant-purchase (100.2.0)  
Downloading: 100%

– Installing magento/module-paypal (100.2.1)  
Downloading: 100%

– Installing magento/module-offline-shipping (100.2.1)  
Downloading: 100%

– Installing magento/module-offline-payments (100.2.0)  
Downloading: 100%

– Installing magento/module-new-relic-reporting (100.2.1)  
Downloading: 100%

– Installing magento/module-multishipping (100.2.0)  
Downloading: 100%

– Installing magento/module-layered-navigation (100.2.0)  
Downloading: 100%

– Installing magento/module-grouped-import-export (100.2.0)  
Downloading: 100%

– Installing magento/module-cookie (100.2.0)  
Downloading: 100%

– Installing magento/module-google-analytics (100.2.1)  
Downloading: 100%

– Installing magento/module-google-optimizer (100.2.1)  
Downloading: 100%

– Installing magento/module-google-adwords (100.2.0)  
Downloading: 100%

– Installing magento/module-fedex (100.2.0)  
Downloading: 100%

– Installing magento/module-encryption-key (100.2.0)  
Downloading: 100%

– Installing magento/module-downloadable-import-export (100.2.0)  
Downloading: 100%

– Installing magento/module-dhl (100.2.0)  
Downloading: 100%

– Installing magento/module-customer-import-export (100.2.1)  
Downloading: 100%

– Installing magento/module-customer-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-currency-symbol (100.2.0)  
Downloading: 100%

– Installing magento/module-configurable-product-sales (100.2.0)  
Downloading: 100%

– Installing magento/module-configurable-import-export (100.2.0)  
Downloading: 100%

– Installing magento/module-checkout-agreements (100.2.0)  
Downloading: 100%

– Installing magento/module-catalog-widget (100.2.0)  
Downloading: 100%

– Installing magento/module-catalog-rule-configurable (100.2.0)  
Downloading: 100%

– Installing magento/module-catalog-analytics (100.2.0)  
Downloading: 100%

– Installing zendframework/zend-session (2.8.5)  
Downloading: 100%

– Installing paragonie/random_compat (v2.0.11)  
Downloading: 100%

– Installing zendframework/zend-captcha (2.7.1)  
Downloading: 100%

– Installing zendframework/zend-db (2.9.2)  
Downloading: 100%

– Installing magento/module-captcha (100.2.0)  
Downloading: 100%

– Installing magento/module-cache-invalidate (100.2.0)  
Downloading: 100%

– Installing magento/module-bundle (100.2.2)  
Downloading: 100%

– Installing magento/module-bundle-import-export (100.2.0)  
Downloading: 100%

– Installing braintree/braintree_php (3.25.0)  
Downloading: 100%

– Installing magento/module-braintree (100.2.2)  
Downloading: 100%

– Installing magento/module-authorizenet (100.2.0)  
Downloading: 100%

– Installing magento/module-analytics (100.2.0)  
Downloading: 100%

– Installing magento/module-advanced-pricing-import-export (100.2.1)  
Downloading: 100%

– Installing magento/module-admin-notification (100.2.1)  
Downloading: 100%

– Installing magento/module-marketplace (100.2.0)  
Downloading: 100%

– Installing ramsey/uuid (3.7.1)  
Downloading: 100%

– Installing league/climate (2.6.1)  
Downloading: 100%

– Installing sjparkinson/static-review (4.1.1)  
Downloading: 100%

– Installing magento/composer (1.2.0)  
Downloading: 100%

– Installing phpseclib/phpseclib (2.0.10)  
Downloading: 100%

– Installing symfony/event-dispatcher (v2.8.36)  
Downloading: 100%

– Installing tubalmartin/cssmin (v4.1.0)  
Downloading: 100%

– Installing pelago/emogrifier (V1.2.0)  
Downloading: 100%

– Installing colinmollenhour/cache-backend-file (1.4)  
Downloading: 100%

– Installing colinmollenhour/cache-backend-redis (1.10.2)  
Downloading: 100%

– Installing zendframework/zend-log (2.9.2)  
Downloading: 100%

– Installing zendframework/zend-json (2.6.1)  
Downloading: 100%

– Installing zendframework/zend-serializer (2.8.1)  
Downloading: 100%

– Installing zendframework/zend-di (2.6.1)  
Downloading: 100%

– Installing zendframework/zend-config (2.6.0)  
Downloading: 100%

– Installing zendframework/zend-view (2.10.0)  
Downloading: 100%

– Installing zendframework/zend-i18n (2.7.4)  
Downloading: 100%

– Installing zendframework/zend-text (2.6.0)  
Downloading: 100%

– Installing zendframework/zend-modulemanager (2.8.2)  
Downloading: 100%

– Installing zendframework/zend-console (2.7.0)  
Downloading: 100%

– Installing zendframework/zend-server (2.7.0)  
Downloading: 100%

– Installing zendframework/zend-soap (2.7.0)  
Downloading: 100%

– Installing magento/magento2-base (2.2.2)  
Downloading: 100%

Package sjparkinson/static-review is abandoned, you should avoid using it. Use phpro/grumphp instead.  
Writing lock file  
Generating autoload files  
Please enter the database host [localhost]: localhost  
Please enter the database port [3306]: 3306  
Please enter the database username [root]: root  
Please enter the database password []: root  
Please enter the database name [magento]: magento2  
Created database magento2  
Please enter the base url: [http://magento2.localdomain/]:magento.test  
Please enter a valid URL  
Please enter the base url: [http://magento2.localdomain/]:http://magento.test/  
Start installation process.  
/usr/local/Cellar/php71/7.1.14_25/bin/php -ddisplay_startup_errors=1 -ddisplay_errors=1 -derror_reporting=-1 -f ‘/Users/kalpesh/sites/magento/bin/magento’ — setup:install –language=’de_DE’ –timezone=’Europe/Berlin’ –db-host=’localhost’ –db-name=’magento2′ –db-user=’root’ –base-url=’http://magento.test/’ –use-rewrites=’1′ –use-secure=’0′ –use-secure-admin=’1′ –admin-user=’admin’ –admin-lastname=’Doe’ –admin-firstname=’John’ –admin-email=’john.doe@example.com’ –admin-password=’password123′ –session-save=’files’ –backend-frontname=’admin’ –currency=’EUR’ –db-password=’root’ –base-url-secure=’https://mage2.test/’  
Successfully installed Magento  
Encryption Key: File permissions check…  
[Progress: 1 / 485]  
Required extensions check…  
[Progress: 2 / 485]  
Enabling Maintenance Mode…  
[Progress: 3 / 485]  
Installing deployment configuration…  
[Progress: 4 / 485]  
Installing database schema:  
Schema creation/updates:  
Module ‘Magento_Store’:  
Installing schema… Upgrading schema…  
[Progress: 5 / 485]  
Module ‘Magento_Directory’:  
Installing schema…  
[Progress: 6 / 485]  
Module ‘Magento_AdvancedPricingImportExport’:  
[Progress: 7 / 485]  
Module ‘Magento_Config’:  
Installing schema…  
[Progress: 8 / 485]  
Module ‘Magento_Backend’:  
[Progress: 9 / 485]  
Module ‘Magento_Theme’:  
Installing schema…  
[Progress: 10 / 485]  
Module ‘Magento_Eav’:  
Installing schema… Upgrading schema…  
[Progress: 11 / 485]  
Module ‘Magento_Backup’:  
[Progress: 12 / 485]  
Module ‘Magento_Customer’:  
Installing schema… Upgrading schema…  
[Progress: 13 / 485]  
Module ‘Magento_AdminNotification’:  
Installing schema…  
[Progress: 14 / 485]  
Module ‘Magento_BundleImportExport’:  
[Progress: 15 / 485]  
Module ‘Magento_CacheInvalidate’:  
[Progress: 16 / 485]  
Module ‘Magento_Indexer’:  
Installing schema…  
[Progress: 17 / 485]  
Module ‘Magento_Cms’:  
Installing schema… Upgrading schema…  
[Progress: 18 / 485]  
Module ‘Magento_Security’:  
Installing schema… Upgrading schema…  
[Progress: 19 / 485]  
Module ‘Magento_CatalogImportExport’:  
[Progress: 20 / 485]  
Module ‘Magento_Rule’:  
[Progress: 21 / 485]  
Module ‘Magento_Cron’:  
Installing schema…  
[Progress: 22 / 485]  
Module ‘Magento_Catalog’:  
Installing schema… Upgrading schema…  
[Progress: 23 / 485]  
Module ‘Magento_Search’:  
Installing schema… Upgrading schema…  
[Progress: 24 / 485]  
Module ‘Magento_CatalogUrlRewrite’:  
Installing schema…  
[Progress: 25 / 485]  
Module ‘Magento_Widget’:  
Installing schema…  
[Progress: 26 / 485]  
Module ‘Magento_Quote’:  
Installing schema… Upgrading schema…  
[Progress: 27 / 485]  
Module ‘Magento_SalesSequence’:  
Installing schema…  
[Progress: 28 / 485]  
Module ‘Magento_Payment’:  
[Progress: 29 / 485]  
Module ‘Magento_CmsUrlRewrite’:  
[Progress: 30 / 485]  
Module ‘Magento_User’:  
Installing schema… Upgrading schema…  
[Progress: 31 / 485]  
Module ‘Magento_ConfigurableImportExport’:  
[Progress: 32 / 485]  
Module ‘Magento_Msrp’:  
[Progress: 33 / 485]  
Module ‘Magento_CatalogInventory’:  
Installing schema… Upgrading schema…  
[Progress: 34 / 485]  
Module ‘Magento_Contact’:  
[Progress: 35 / 485]  
Module ‘Magento_Cookie’:  
[Progress: 36 / 485]  
Module ‘Magento_Newsletter’:  
Installing schema…  
[Progress: 37 / 485]  
Module ‘Magento_CurrencySymbol’:  
[Progress: 38 / 485]  
Module ‘Magento_Sales’:  
Installing schema… Upgrading schema…  
[Progress: 39 / 485]  
Module ‘Magento_Integration’:  
Installing schema… Upgrading schema…  
[Progress: 40 / 485]  
Module ‘Magento_CustomerImportExport’:  
[Progress: 41 / 485]  
Module ‘Magento_Deploy’:  
[Progress: 42 / 485]  
Module ‘Magento_Developer’:  
[Progress: 43 / 485]  
Module ‘Magento_Dhl’:  
[Progress: 44 / 485]  
Module ‘Magento_Authorization’:  
Installing schema…  
[Progress: 45 / 485]  
Module ‘Magento_Downloadable’:  
Installing schema… Upgrading schema…  
[Progress: 46 / 485]  
Module ‘Magento_ImportExport’:  
Installing schema… Upgrading schema…  
[Progress: 47 / 485]  
Module ‘Magento_Bundle’:  
Installing schema… Upgrading schema…  
[Progress: 48 / 485]  
Module ‘Magento_Email’:  
Installing schema…  
[Progress: 49 / 485]  
Module ‘Magento_EncryptionKey’:  
[Progress: 50 / 485]  
Module ‘Magento_Fedex’:  
[Progress: 51 / 485]  
Module ‘Magento_GiftMessage’:  
Installing schema…  
[Progress: 52 / 485]  
Module ‘Magento_Checkout’:  
[Progress: 53 / 485]  
Module ‘Magento_GoogleAnalytics’:  
[Progress: 54 / 485]  
Module ‘Magento_Ui’:  
Installing schema…  
[Progress: 55 / 485]  
Module ‘Magento_GroupedImportExport’:  
[Progress: 56 / 485]  
Module ‘Magento_GroupedProduct’:  
[Progress: 57 / 485]  
Module ‘Magento_DownloadableImportExport’:  
[Progress: 58 / 485]  
Module ‘Magento_CatalogRule’:  
Installing schema… Upgrading schema…  
[Progress: 59 / 485]  
Module ‘Magento_InstantPurchase’:  
[Progress: 60 / 485]  
Module ‘Magento_Analytics’:  
[Progress: 61 / 485]  
Module ‘Magento_LayeredNavigation’:  
[Progress: 62 / 485]  
Module ‘Magento_Marketplace’:  
[Progress: 63 / 485]  
Module ‘Magento_MediaStorage’:  
[Progress: 64 / 485]  
Module ‘Magento_ConfigurableProduct’:  
Installing schema…  
[Progress: 65 / 485]  
Module ‘Magento_Multishipping’:  
[Progress: 66 / 485]  
Module ‘Magento_NewRelicReporting’:  
Installing schema… Upgrading schema…  
[Progress: 67 / 485]  
Module ‘Magento_Reports’:  
Installing schema…  
[Progress: 68 / 485]  
Module ‘Magento_OfflinePayments’:  
[Progress: 69 / 485]  
Module ‘Magento_SalesRule’:  
Installing schema… Upgrading schema…  
[Progress: 70 / 485]  
Module ‘Magento_PageCache’:  
[Progress: 71 / 485]  
Module ‘Magento_Vault’:  
Installing schema…  
[Progress: 72 / 485]  
Module ‘Magento_Paypal’:  
Installing schema… Upgrading schema…  
[Progress: 73 / 485]  
Module ‘Magento_Persistent’:  
Installing schema…  
[Progress: 74 / 485]  
Module ‘Magento_ProductAlert’:  
Installing schema…  
[Progress: 75 / 485]  
Module ‘Magento_ProductVideo’:  
Installing schema…  
[Progress: 76 / 485]  
Module ‘Magento_CheckoutAgreements’:  
Installing schema… Upgrading schema…  
[Progress: 77 / 485]  
Module ‘Magento_QuoteAnalytics’:  
[Progress: 78 / 485]  
Module ‘Magento_ReleaseNotification’:  
Installing schema…  
[Progress: 79 / 485]  
Module ‘Magento_Review’:  
Installing schema…  
[Progress: 80 / 485]  
Module ‘Magento_RequireJs’:  
[Progress: 81 / 485]  
Module ‘Magento_Shipping’:  
[Progress: 82 / 485]  
Module ‘Magento_ReviewAnalytics’:  
[Progress: 83 / 485]  
Module ‘Magento_Robots’:  
[Progress: 84 / 485]  
Module ‘Magento_Rss’:  
[Progress: 85 / 485]  
Module ‘Magento_CatalogRuleConfigurable’:  
[Progress: 86 / 485]  
Module ‘Magento_Captcha’:  
Installing schema…  
[Progress: 87 / 485]  
Module ‘Magento_SalesAnalytics’:  
[Progress: 88 / 485]  
Module ‘Magento_SalesInventory’:  
[Progress: 89 / 485]  
Module ‘Magento_OfflineShipping’:  
Installing schema… Upgrading schema…  
[Progress: 90 / 485]  
Module ‘Magento_ConfigurableProductSales’:  
[Progress: 91 / 485]  
Module ‘Magento_UrlRewrite’:  
Installing schema…  
[Progress: 92 / 485]  
Module ‘Magento_CatalogSearch’:  
Installing schema…  
[Progress: 93 / 485]  
Module ‘Magento_CustomerAnalytics’:  
[Progress: 94 / 485]  
Module ‘Magento_SendFriend’:  
Installing schema…  
[Progress: 95 / 485]  
Module ‘Magento_Wishlist’:  
Installing schema…  
[Progress: 96 / 485]  
Module ‘Magento_Signifyd’:  
Installing schema…  
[Progress: 97 / 485]  
Module ‘Magento_Sitemap’:  
Installing schema…  
[Progress: 98 / 485]  
Module ‘Magento_Authorizenet’:  
[Progress: 99 / 485]  
Module ‘Magento_Swagger’:  
[Progress: 100 / 485]  
Module ‘Magento_Swatches’:  
Installing schema…  
[Progress: 101 / 485]  
Module ‘Magento_SwatchesLayeredNavigation’:  
[Progress: 102 / 485]  
Module ‘Magento_Tax’:  
Installing schema…  
[Progress: 103 / 485]  
Module ‘Magento_TaxImportExport’:  
[Progress: 104 / 485]  
Module ‘Magento_GoogleAdwords’:  
[Progress: 105 / 485]  
Module ‘Magento_Translation’:  
Installing schema…  
[Progress: 106 / 485]  
Module ‘Magento_GoogleOptimizer’:  
Installing schema…  
[Progress: 107 / 485]  
Module ‘Magento_Ups’:  
[Progress: 108 / 485]  
Module ‘Magento_SampleData’:  
[Progress: 109 / 485]  
Module ‘Magento_CatalogAnalytics’:  
[Progress: 110 / 485]  
Module ‘Magento_Usps’:  
[Progress: 111 / 485]  
Module ‘Magento_Variable’:  
Installing schema…  
[Progress: 112 / 485]  
Module ‘Magento_Braintree’:  
[Progress: 113 / 485]  
Module ‘Magento_Version’:  
[Progress: 114 / 485]  
Module ‘Magento_Webapi’:  
[Progress: 115 / 485]  
Module ‘Magento_WebapiSecurity’:  
[Progress: 116 / 485]  
Module ‘Magento_Weee’:  
Installing schema…  
[Progress: 117 / 485]  
Module ‘Magento_CatalogWidget’:  
[Progress: 118 / 485]  
Module ‘Dotdigitalgroup_Email’:  
Installing schema… Upgrading schema…  
[Progress: 119 / 485]  
Module ‘Magento_WishlistAnalytics’:  
[Progress: 120 / 485]  
Module ‘Shopial_Facebook’:  
[Progress: 121 / 485]  
Module ‘Temando_Shipping’:  
Installing schema… Upgrading schema…  
[Progress: 122 / 485]  
Schema post-updates:  
Module ‘Magento_Store’:  
[Progress: 123 / 485]  
Module ‘Magento_Directory’:  
[Progress: 124 / 485]  
Module ‘Magento_AdvancedPricingImportExport’:  
[Progress: 125 / 485]  
Module ‘Magento_Config’:  
[Progress: 126 / 485]  
Module ‘Magento_Backend’:  
[Progress: 127 / 485]  
Module ‘Magento_Theme’:  
[Progress: 128 / 485]  
Module ‘Magento_Eav’:  
[Progress: 129 / 485]  
Module ‘Magento_Backup’:  
[Progress: 130 / 485]  
Module ‘Magento_Customer’:  
[Progress: 131 / 485]  
Module ‘Magento_AdminNotification’:  
[Progress: 132 / 485]  
Module ‘Magento_BundleImportExport’:  
[Progress: 133 / 485]  
Module ‘Magento_CacheInvalidate’:  
[Progress: 134 / 485]  
Module ‘Magento_Indexer’:  
Running schema recurring…  
[Progress: 135 / 485]  
Module ‘Magento_Cms’:  
[Progress: 136 / 485]  
Module ‘Magento_Security’:  
[Progress: 137 / 485]  
Module ‘Magento_CatalogImportExport’:  
[Progress: 138 / 485]  
Module ‘Magento_Rule’:  
[Progress: 139 / 485]  
Module ‘Magento_Cron’:  
Running schema recurring…  
[Progress: 140 / 485]  
Module ‘Magento_Catalog’:  
Running schema recurring…  
[Progress: 141 / 485]  
Module ‘Magento_Search’:  
[Progress: 142 / 485]  
Module ‘Magento_CatalogUrlRewrite’:  
Running schema recurring…  
[Progress: 143 / 485]  
Module ‘Magento_Widget’:  
[Progress: 144 / 485]  
Module ‘Magento_Quote’:  
[Progress: 145 / 485]  
Module ‘Magento_SalesSequence’:  
[Progress: 146 / 485]  
Module ‘Magento_Payment’:  
[Progress: 147 / 485]  
Module ‘Magento_CmsUrlRewrite’:  
[Progress: 148 / 485]  
Module ‘Magento_User’:  
[Progress: 149 / 485]  
Module ‘Magento_ConfigurableImportExport’:  
[Progress: 150 / 485]  
Module ‘Magento_Msrp’:  
[Progress: 151 / 485]  
Module ‘Magento_CatalogInventory’:  
Running schema recurring…  
[Progress: 152 / 485]  
Module ‘Magento_Contact’:  
[Progress: 153 / 485]  
Module ‘Magento_Cookie’:  
[Progress: 154 / 485]  
Module ‘Magento_Newsletter’:  
[Progress: 155 / 485]  
Module ‘Magento_CurrencySymbol’:  
[Progress: 156 / 485]  
Module ‘Magento_Sales’:  
[Progress: 157 / 485]  
Module ‘Magento_Integration’:  
Running schema recurring…  
[Progress: 158 / 485]  
Module ‘Magento_CustomerImportExport’:  
[Progress: 159 / 485]  
Module ‘Magento_Deploy’:  
[Progress: 160 / 485]  
Module ‘Magento_Developer’:  
[Progress: 161 / 485]  
Module ‘Magento_Dhl’:  
[Progress: 162 / 485]  
Module ‘Magento_Authorization’:  
[Progress: 163 / 485]  
Module ‘Magento_Downloadable’:  
[Progress: 164 / 485]  
Module ‘Magento_ImportExport’:  
[Progress: 165 / 485]  
Module ‘Magento_Bundle’:  
Running schema recurring…  
[Progress: 166 / 485]  
Module ‘Magento_Email’:  
[Progress: 167 / 485]  
Module ‘Magento_EncryptionKey’:  
[Progress: 168 / 485]  
Module ‘Magento_Fedex’:  
[Progress: 169 / 485]  
Module ‘Magento_GiftMessage’:  
[Progress: 170 / 485]  
Module ‘Magento_Checkout’:  
[Progress: 171 / 485]  
Module ‘Magento_GoogleAnalytics’:  
[Progress: 172 / 485]  
Module ‘Magento_Ui’:  
[Progress: 173 / 485]  
Module ‘Magento_GroupedImportExport’:  
[Progress: 174 / 485]  
Module ‘Magento_GroupedProduct’:  
[Progress: 175 / 485]  
Module ‘Magento_DownloadableImportExport’:  
[Progress: 176 / 485]  
Module ‘Magento_CatalogRule’:  
[Progress: 177 / 485]  
Module ‘Magento_InstantPurchase’:  
[Progress: 178 / 485]  
Module ‘Magento_Analytics’:  
[Progress: 179 / 485]  
Module ‘Magento_LayeredNavigation’:  
[Progress: 180 / 485]  
Module ‘Magento_Marketplace’:  
[Progress: 181 / 485]  
Module ‘Magento_MediaStorage’:  
[Progress: 182 / 485]  
Module ‘Magento_ConfigurableProduct’:  
Running schema recurring…  
[Progress: 183 / 485]  
Module ‘Magento_Multishipping’:  
[Progress: 184 / 485]  
Module ‘Magento_NewRelicReporting’:  
[Progress: 185 / 485]  
Module ‘Magento_Reports’:  
Running schema recurring…  
[Progress: 186 / 485]  
Module ‘Magento_OfflinePayments’:  
[Progress: 187 / 485]  
Module ‘Magento_SalesRule’:  
[Progress: 188 / 485]  
Module ‘Magento_PageCache’:  
[Progress: 189 / 485]  
Module ‘Magento_Vault’:  
[Progress: 190 / 485]  
Module ‘Magento_Paypal’:  
[Progress: 191 / 485]  
Module ‘Magento_Persistent’:  
[Progress: 192 / 485]  
Module ‘Magento_ProductAlert’:  
Running schema recurring…  
[Progress: 193 / 485]  
Module ‘Magento_ProductVideo’:  
[Progress: 194 / 485]  
Module ‘Magento_CheckoutAgreements’:  
[Progress: 195 / 485]  
Module ‘Magento_QuoteAnalytics’:  
[Progress: 196 / 485]  
Module ‘Magento_ReleaseNotification’:  
[Progress: 197 / 485]  
Module ‘Magento_Review’:  
[Progress: 198 / 485]  
Module ‘Magento_RequireJs’:  
[Progress: 199 / 485]  
Module ‘Magento_Shipping’:  
[Progress: 200 / 485]  
Module ‘Magento_ReviewAnalytics’:  
[Progress: 201 / 485]  
Module ‘Magento_Robots’:  
[Progress: 202 / 485]  
Module ‘Magento_Rss’:  
[Progress: 203 / 485]  
Module ‘Magento_CatalogRuleConfigurable’:  
[Progress: 204 / 485]  
Module ‘Magento_Captcha’:  
[Progress: 205 / 485]  
Module ‘Magento_SalesAnalytics’:  
[Progress: 206 / 485]  
Module ‘Magento_SalesInventory’:  
[Progress: 207 / 485]  
Module ‘Magento_OfflineShipping’:  
[Progress: 208 / 485]  
Module ‘Magento_ConfigurableProductSales’:  
[Progress: 209 / 485]  
Module ‘Magento_UrlRewrite’:  
[Progress: 210 / 485]  
Module ‘Magento_CatalogSearch’:  
[Progress: 211 / 485]  
Module ‘Magento_CustomerAnalytics’:  
[Progress: 212 / 485]  
Module ‘Magento_SendFriend’:  
[Progress: 213 / 485]  
Module ‘Magento_Wishlist’:  
Running schema recurring…  
[Progress: 214 / 485]  
Module ‘Magento_Signifyd’:  
[Progress: 215 / 485]  
Module ‘Magento_Sitemap’:  
[Progress: 216 / 485]  
Module ‘Magento_Authorizenet’:  
[Progress: 217 / 485]  
Module ‘Magento_Swagger’:  
[Progress: 218 / 485]  
Module ‘Magento_Swatches’:  
[Progress: 219 / 485]  
Module ‘Magento_SwatchesLayeredNavigation’:  
[Progress: 220 / 485]  
Module ‘Magento_Tax’:  
[Progress: 221 / 485]  
Module ‘Magento_TaxImportExport’:  
[Progress: 222 / 485]  
Module ‘Magento_GoogleAdwords’:  
[Progress: 223 / 485]  
Module ‘Magento_Translation’:  
[Progress: 224 / 485]  
Module ‘Magento_GoogleOptimizer’:  
[Progress: 225 / 485]  
Module ‘Magento_Ups’:  
[Progress: 226 / 485]  
Module ‘Magento_SampleData’:  
[Progress: 227 / 485]  
Module ‘Magento_CatalogAnalytics’:  
[Progress: 228 / 485]  
Module ‘Magento_Usps’:  
[Progress: 229 / 485]  
Module ‘Magento_Variable’:  
[Progress: 230 / 485]  
Module ‘Magento_Braintree’:  
[Progress: 231 / 485]  
Module ‘Magento_Version’:  
[Progress: 232 / 485]  
Module ‘Magento_Webapi’:  
[Progress: 233 / 485]  
Module ‘Magento_WebapiSecurity’:  
[Progress: 234 / 485]  
Module ‘Magento_Weee’:  
Running schema recurring…  
[Progress: 235 / 485]  
Module ‘Magento_CatalogWidget’:  
[Progress: 236 / 485]  
Module ‘Dotdigitalgroup_Email’:  
Running schema recurring…  
[Progress: 237 / 485]  
Module ‘Magento_WishlistAnalytics’:  
[Progress: 238 / 485]  
Module ‘Shopial_Facebook’:  
[Progress: 239 / 485]  
Module ‘Temando_Shipping’:  
[Progress: 240 / 485]  
[Progress: 241 / 485]  
Installing user configuration…  
[Progress: 242 / 485]  
Enabling caches:  
Current status:  
Array  
(  
[config] => 1  
[layout] => 1  
[block_html] => 1  
[collections] => 1  
[reflection] => 1  
[db_ddl] => 1  
[eav] => 1  
[customer_notification] => 1  
[config_integration] => 1  
[config_integration_api] => 1  
[full_page] => 1  
[translate] => 1  
[config_webservice] => 1  
)

[Progress: 243 / 485]  
Installing data…  
Data install/update:  
Module ‘Magento_Store’:  
Upgrading data…  
[Progress: 244 / 485]  
Module ‘Magento_Directory’:  
Installing data… Upgrading data…  
[Progress: 245 / 485]  
Module ‘Magento_AdvancedPricingImportExport’:  
[Progress: 246 / 485]  
Module ‘Magento_Config’:  
Installing data…  
[Progress: 247 / 485]  
Module ‘Magento_Backend’:  
[Progress: 248 / 485]  
Module ‘Magento_Theme’:  
Installing data… Upgrading data…  
[Progress: 249 / 485]  
Module ‘Magento_Eav’:  
Installing data…  
[Progress: 250 / 485]  
Module ‘Magento_Backup’:  
[Progress: 251 / 485]  
Module ‘Magento_Customer’:  
Installing data… Upgrading data…  
[Progress: 252 / 485]  
Module ‘Magento_AdminNotification’:  
[Progress: 253 / 485]  
Module ‘Magento_BundleImportExport’:  
[Progress: 254 / 485]  
Module ‘Magento_CacheInvalidate’:  
[Progress: 255 / 485]  
Module ‘Magento_Indexer’:  
Installing data…  
[Progress: 256 / 485]  
Module ‘Magento_Cms’:  
Installing data… Upgrading data…  
[Progress: 257 / 485]  
Module ‘Magento_Security’:  
[Progress: 258 / 485]  
Module ‘Magento_CatalogImportExport’:  
[Progress: 259 / 485]  
Module ‘Magento_Rule’:  
[Progress: 260 / 485]  
Module ‘Magento_Cron’:  
[Progress: 261 / 485]  
Module ‘Magento_Catalog’:  
Installing data… Upgrading data…  
[Progress: 262 / 485]  
Module ‘Magento_Search’:  
[Progress: 263 / 485]  
Module ‘Magento_CatalogUrlRewrite’:  
Installing data…  
[Progress: 264 / 485]  
Module ‘Magento_Widget’:  
Installing data… Upgrading data…  
[Progress: 265 / 485]  
Module ‘Magento_Quote’:  
Installing data… Upgrading data…  
[Progress: 266 / 485]  
Module ‘Magento_SalesSequence’:  
Installing data…  
[Progress: 267 / 485]  
Module ‘Magento_Payment’:  
[Progress: 268 / 485]  
Module ‘Magento_CmsUrlRewrite’:  
[Progress: 269 / 485]  
Module ‘Magento_User’:  
Upgrading data…  
[Progress: 270 / 485]  
Module ‘Magento_ConfigurableImportExport’:  
[Progress: 271 / 485]  
Module ‘Magento_Msrp’:  
Installing data… Upgrading data…  
[Progress: 272 / 485]  
Module ‘Magento_CatalogInventory’:  
Installing data… Upgrading data…  
[Progress: 273 / 485]  
Module ‘Magento_Contact’:  
[Progress: 274 / 485]  
Module ‘Magento_Cookie’:  
[Progress: 275 / 485]  
Module ‘Magento_Newsletter’:  
[Progress: 276 / 485]  
Module ‘Magento_CurrencySymbol’:  
Upgrading data…  
[Progress: 277 / 485]  
Module ‘Magento_Sales’:  
Installing data… Upgrading data…  
[Progress: 278 / 485]  
Module ‘Magento_Integration’:  
Upgrading data…  
[Progress: 279 / 485]  
Module ‘Magento_CustomerImportExport’:  
[Progress: 280 / 485]  
Module ‘Magento_Deploy’:  
[Progress: 281 / 485]  
Module ‘Magento_Developer’:  
[Progress: 282 / 485]  
Module ‘Magento_Dhl’:  
Installing data…  
[Progress: 283 / 485]  
Module ‘Magento_Authorization’:  
Installing data…  
[Progress: 284 / 485]  
Module ‘Magento_Downloadable’:  
Installing data…  
[Progress: 285 / 485]  
Module ‘Magento_ImportExport’:  
[Progress: 286 / 485]  
Module ‘Magento_Bundle’:  
Installing data… Upgrading data…  
[Progress: 287 / 485]  
Module ‘Magento_Email’:  
[Progress: 288 / 485]  
Module ‘Magento_EncryptionKey’:  
[Progress: 289 / 485]  
Module ‘Magento_Fedex’:  
Installing data…  
[Progress: 290 / 485]  
Module ‘Magento_GiftMessage’:  
Installing data… Upgrading data…  
[Progress: 291 / 485]  
Module ‘Magento_Checkout’:  
Installing data…  
[Progress: 292 / 485]  
Module ‘Magento_GoogleAnalytics’:  
[Progress: 293 / 485]  
Module ‘Magento_Ui’:  
[Progress: 294 / 485]  
Module ‘Magento_GroupedImportExport’:  
[Progress: 295 / 485]  
Module ‘Magento_GroupedProduct’:  
Installing data… Upgrading data…  
[Progress: 296 / 485]  
Module ‘Magento_DownloadableImportExport’:  
[Progress: 297 / 485]  
Module ‘Magento_CatalogRule’:  
Installing data… Upgrading data…  
[Progress: 298 / 485]  
Module ‘Magento_InstantPurchase’:  
[Progress: 299 / 485]  
Module ‘Magento_Analytics’:  
Installing data…  
[Progress: 300 / 485]  
Module ‘Magento_LayeredNavigation’:  
[Progress: 301 / 485]  
Module ‘Magento_Marketplace’:  
[Progress: 302 / 485]  
Module ‘Magento_MediaStorage’:  
[Progress: 303 / 485]  
Module ‘Magento_ConfigurableProduct’:  
Installing data… Upgrading data…  
[Progress: 304 / 485]  
Module ‘Magento_Multishipping’:  
[Progress: 305 / 485]  
Module ‘Magento_NewRelicReporting’:  
[Progress: 306 / 485]  
Module ‘Magento_Reports’:  
Installing data…  
[Progress: 307 / 485]  
Module ‘Magento_OfflinePayments’:  
[Progress: 308 / 485]  
Module ‘Magento_SalesRule’:  
Installing data… Upgrading data…  
[Progress: 309 / 485]  
Module ‘Magento_PageCache’:  
[Progress: 310 / 485]  
Module ‘Magento_Vault’:  
Upgrading data…  
[Progress: 311 / 485]  
Module ‘Magento_Paypal’:  
Installing data…  
[Progress: 312 / 485]  
Module ‘Magento_Persistent’:  
[Progress: 313 / 485]  
Module ‘Magento_ProductAlert’:  
[Progress: 314 / 485]  
Module ‘Magento_ProductVideo’:  
[Progress: 315 / 485]  
Module ‘Magento_CheckoutAgreements’:  
[Progress: 316 / 485]  
Module ‘Magento_QuoteAnalytics’:  
[Progress: 317 / 485]  
Module ‘Magento_ReleaseNotification’:  
[Progress: 318 / 485]  
Module ‘Magento_Review’:  
Installing data…  
[Progress: 319 / 485]  
Module ‘Magento_RequireJs’:  
[Progress: 320 / 485]  
Module ‘Magento_Shipping’:  
[Progress: 321 / 485]  
Module ‘Magento_ReviewAnalytics’:  
[Progress: 322 / 485]  
Module ‘Magento_Robots’:  
[Progress: 323 / 485]  
Module ‘Magento_Rss’:  
[Progress: 324 / 485]  
Module ‘Magento_CatalogRuleConfigurable’:  
[Progress: 325 / 485]  
Module ‘Magento_Captcha’:  
[Progress: 326 / 485]  
Module ‘Magento_SalesAnalytics’:  
[Progress: 327 / 485]  
Module ‘Magento_SalesInventory’:  
[Progress: 328 / 485]  
Module ‘Magento_OfflineShipping’:  
Upgrading data…  
[Progress: 329 / 485]  
Module ‘Magento_ConfigurableProductSales’:  
[Progress: 330 / 485]  
Module ‘Magento_UrlRewrite’:  
Upgrading data…  
[Progress: 331 / 485]  
Module ‘Magento_CatalogSearch’:  
Installing data…  
[Progress: 332 / 485]  
Module ‘Magento_CustomerAnalytics’:  
[Progress: 333 / 485]  
Module ‘Magento_SendFriend’:  
[Progress: 334 / 485]  
Module ‘Magento_Wishlist’:  
Upgrading data…  
[Progress: 335 / 485]  
Module ‘Magento_Signifyd’:  
[Progress: 336 / 485]  
Module ‘Magento_Sitemap’:  
[Progress: 337 / 485]  
Module ‘Magento_Authorizenet’:  
[Progress: 338 / 485]  
Module ‘Magento_Swagger’:  
[Progress: 339 / 485]  
Module ‘Magento_Swatches’:  
Installing data… Upgrading data…  
[Progress: 340 / 485]  
Module ‘Magento_SwatchesLayeredNavigation’:  
[Progress: 341 / 485]  
Module ‘Magento_Tax’:  
Installing data… Upgrading data…  
[Progress: 342 / 485]  
Module ‘Magento_TaxImportExport’:  
[Progress: 343 / 485]  
Module ‘Magento_GoogleAdwords’:  
[Progress: 344 / 485]  
Module ‘Magento_Translation’:  
[Progress: 345 / 485]  
Module ‘Magento_GoogleOptimizer’:  
[Progress: 346 / 485]  
Module ‘Magento_Ups’:  
[Progress: 347 / 485]  
Module ‘Magento_SampleData’:  
Installing data…  
[Progress: 348 / 485]  
Module ‘Magento_CatalogAnalytics’:  
[Progress: 349 / 485]  
Module ‘Magento_Usps’:  
Upgrading data…  
[Progress: 350 / 485]  
Module ‘Magento_Variable’:  
[Progress: 351 / 485]  
Module ‘Magento_Braintree’:  
Upgrading data…  
[Progress: 352 / 485]  
Module ‘Magento_Version’:  
[Progress: 353 / 485]  
Module ‘Magento_Webapi’:  
[Progress: 354 / 485]  
Module ‘Magento_WebapiSecurity’:  
[Progress: 355 / 485]  
Module ‘Magento_Weee’:  
Installing data…  
[Progress: 356 / 485]  
Module ‘Magento_CatalogWidget’:  
[Progress: 357 / 485]  
Module ‘Dotdigitalgroup_Email’:  
Installing data…  
[Progress: 358 / 485]  
Module ‘Magento_WishlistAnalytics’:  
[Progress: 359 / 485]  
Module ‘Shopial_Facebook’:  
[Progress: 360 / 485]  
Module ‘Temando_Shipping’:  
[Progress: 361 / 485]  
Data post-updates:  
Module ‘Magento_Store’:  
[Progress: 362 / 485]  
Module ‘Magento_Directory’:  
[Progress: 363 / 485]  
Module ‘Magento_AdvancedPricingImportExport’:  
[Progress: 364 / 485]  
Module ‘Magento_Config’:  
[Progress: 365 / 485]  
Module ‘Magento_Backend’:  
[Progress: 366 / 485]  
Module ‘Magento_Theme’:  
Running data recurring…  
[Progress: 367 / 485]  
Module ‘Magento_Eav’:  
[Progress: 368 / 485]  
Module ‘Magento_Backup’:  
[Progress: 369 / 485]  
Module ‘Magento_Customer’:  
[Progress: 370 / 485]  
Module ‘Magento_AdminNotification’:  
[Progress: 371 / 485]  
Module ‘Magento_BundleImportExport’:  
[Progress: 372 / 485]  
Module ‘Magento_CacheInvalidate’:  
[Progress: 373 / 485]  
Module ‘Magento_Indexer’:  
Running data recurring…  
[Progress: 374 / 485]  
Module ‘Magento_Cms’:  
[Progress: 375 / 485]  
Module ‘Magento_Security’:  
[Progress: 376 / 485]  
Module ‘Magento_CatalogImportExport’:  
[Progress: 377 / 485]  
Module ‘Magento_Rule’:  
[Progress: 378 / 485]  
Module ‘Magento_Cron’:  
[Progress: 379 / 485]  
Module ‘Magento_Catalog’:  
[Progress: 380 / 485]  
Module ‘Magento_Search’:  
[Progress: 381 / 485]  
Module ‘Magento_CatalogUrlRewrite’:  
[Progress: 382 / 485]  
Module ‘Magento_Widget’:  
[Progress: 383 / 485]  
Module ‘Magento_Quote’:  
[Progress: 384 / 485]  
Module ‘Magento_SalesSequence’:  
Running data recurring…  
[Progress: 385 / 485]  
Module ‘Magento_Payment’:  
[Progress: 386 / 485]  
Module ‘Magento_CmsUrlRewrite’:  
[Progress: 387 / 485]  
Module ‘Magento_User’:  
[Progress: 388 / 485]  
Module ‘Magento_ConfigurableImportExport’:  
[Progress: 389 / 485]  
Module ‘Magento_Msrp’:  
[Progress: 390 / 485]  
Module ‘Magento_CatalogInventory’:  
[Progress: 391 / 485]  
Module ‘Magento_Contact’:  
[Progress: 392 / 485]  
Module ‘Magento_Cookie’:  
[Progress: 393 / 485]  
Module ‘Magento_Newsletter’:  
[Progress: 394 / 485]  
Module ‘Magento_CurrencySymbol’:  
[Progress: 395 / 485]  
Module ‘Magento_Sales’:  
[Progress: 396 / 485]  
Module ‘Magento_Integration’:  
[Progress: 397 / 485]  
Module ‘Magento_CustomerImportExport’:  
[Progress: 398 / 485]  
Module ‘Magento_Deploy’:  
[Progress: 399 / 485]  
Module ‘Magento_Developer’:  
[Progress: 400 / 485]  
Module ‘Magento_Dhl’:  
[Progress: 401 / 485]  
Module ‘Magento_Authorization’:  
[Progress: 402 / 485]  
Module ‘Magento_Downloadable’:  
[Progress: 403 / 485]  
Module ‘Magento_ImportExport’:  
[Progress: 404 / 485]  
Module ‘Magento_Bundle’:  
[Progress: 405 / 485]  
Module ‘Magento_Email’:  
[Progress: 406 / 485]  
Module ‘Magento_EncryptionKey’:  
[Progress: 407 / 485]  
Module ‘Magento_Fedex’:  
[Progress: 408 / 485]  
Module ‘Magento_GiftMessage’:  
[Progress: 409 / 485]  
Module ‘Magento_Checkout’:  
[Progress: 410 / 485]  
Module ‘Magento_GoogleAnalytics’:  
[Progress: 411 / 485]  
Module ‘Magento_Ui’:  
[Progress: 412 / 485]  
Module ‘Magento_GroupedImportExport’:  
[Progress: 413 / 485]  
Module ‘Magento_GroupedProduct’:  
[Progress: 414 / 485]  
Module ‘Magento_DownloadableImportExport’:  
[Progress: 415 / 485]  
Module ‘Magento_CatalogRule’:  
[Progress: 416 / 485]  
Module ‘Magento_InstantPurchase’:  
[Progress: 417 / 485]  
Module ‘Magento_Analytics’:  
[Progress: 418 / 485]  
Module ‘Magento_LayeredNavigation’:  
[Progress: 419 / 485]  
Module ‘Magento_Marketplace’:  
[Progress: 420 / 485]  
Module ‘Magento_MediaStorage’:  
[Progress: 421 / 485]  
Module ‘Magento_ConfigurableProduct’:  
[Progress: 422 / 485]  
Module ‘Magento_Multishipping’:  
[Progress: 423 / 485]  
Module ‘Magento_NewRelicReporting’:  
[Progress: 424 / 485]  
Module ‘Magento_Reports’:  
[Progress: 425 / 485]  
Module ‘Magento_OfflinePayments’:  
[Progress: 426 / 485]  
Module ‘Magento_SalesRule’:  
[Progress: 427 / 485]  
Module ‘Magento_PageCache’:  
[Progress: 428 / 485]  
Module ‘Magento_Vault’:  
[Progress: 429 / 485]  
Module ‘Magento_Paypal’:  
[Progress: 430 / 485]  
Module ‘Magento_Persistent’:  
[Progress: 431 / 485]  
Module ‘Magento_ProductAlert’:  
[Progress: 432 / 485]  
Module ‘Magento_ProductVideo’:  
[Progress: 433 / 485]  
Module ‘Magento_CheckoutAgreements’:  
[Progress: 434 / 485]  
Module ‘Magento_QuoteAnalytics’:  
[Progress: 435 / 485]  
Module ‘Magento_ReleaseNotification’:  
[Progress: 436 / 485]  
Module ‘Magento_Review’:  
[Progress: 437 / 485]  
Module ‘Magento_RequireJs’:  
[Progress: 438 / 485]  
Module ‘Magento_Shipping’:  
[Progress: 439 / 485]  
Module ‘Magento_ReviewAnalytics’:  
[Progress: 440 / 485]  
Module ‘Magento_Robots’:  
[Progress: 441 / 485]  
Module ‘Magento_Rss’:  
[Progress: 442 / 485]  
Module ‘Magento_CatalogRuleConfigurable’:  
[Progress: 443 / 485]  
Module ‘Magento_Captcha’:  
[Progress: 444 / 485]  
Module ‘Magento_SalesAnalytics’:  
[Progress: 445 / 485]  
Module ‘Magento_SalesInventory’:  
[Progress: 446 / 485]  
Module ‘Magento_OfflineShipping’:  
[Progress: 447 / 485]  
Module ‘Magento_ConfigurableProductSales’:  
[Progress: 448 / 485]  
Module ‘Magento_UrlRewrite’:  
[Progress: 449 / 485]  
Module ‘Magento_CatalogSearch’:  
[Progress: 450 / 485]  
Module ‘Magento_CustomerAnalytics’:  
[Progress: 451 / 485]  
Module ‘Magento_SendFriend’:  
[Progress: 452 / 485]  
Module ‘Magento_Wishlist’:  
[Progress: 453 / 485]  
Module ‘Magento_Signifyd’:  
[Progress: 454 / 485]  
Module ‘Magento_Sitemap’:  
[Progress: 455 / 485]  
Module ‘Magento_Authorizenet’:  
[Progress: 456 / 485]  
Module ‘Magento_Swagger’:  
[Progress: 457 / 485]  
Module ‘Magento_Swatches’:  
[Progress: 458 / 485]  
Module ‘Magento_SwatchesLayeredNavigation’:  
[Progress: 459 / 485]  
Module ‘Magento_Tax’:  
[Progress: 460 / 485]  
Module ‘Magento_TaxImportExport’:  
[Progress: 461 / 485]  
Module ‘Magento_GoogleAdwords’:  
[Progress: 462 / 485]  
Module ‘Magento_Translation’:  
[Progress: 463 / 485]  
Module ‘Magento_GoogleOptimizer’:  
[Progress: 464 / 485]  
Module ‘Magento_Ups’:  
[Progress: 465 / 485]  
Module ‘Magento_SampleData’:  
[Progress: 466 / 485]  
Module ‘Magento_CatalogAnalytics’:  
[Progress: 467 / 485]  
Module ‘Magento_Usps’:  
[Progress: 468 / 485]  
Module ‘Magento_Variable’:  
[Progress: 469 / 485]  
Module ‘Magento_Braintree’:  
[Progress: 470 / 485]  
Module ‘Magento_Version’:  
[Progress: 471 / 485]  
Module ‘Magento_Webapi’:  
[Progress: 472 / 485]  
Module ‘Magento_WebapiSecurity’:  
[Progress: 473 / 485]  
Module ‘Magento_Weee’:  
[Progress: 474 / 485]  
Module ‘Magento_CatalogWidget’:  
[Progress: 475 / 485]  
Module ‘Dotdigitalgroup_Email’:  
[Progress: 476 / 485]  
Module ‘Magento_WishlistAnalytics’:  
[Progress: 477 / 485]  
Module ‘Shopial_Facebook’:  
[Progress: 478 / 485]  
Module ‘Temando_Shipping’:  
[Progress: 479 / 485]  
[Progress: 480 / 485]  
Installing admin user…  
[Progress: 481 / 485]  
Caches clearing:  
Cache cleared successfully  
[Progress: 482 / 485]  
Disabling Maintenance Mode:  
[Progress: 483 / 485]  
Post installation file permissions check…  
For security, remove write permissions from these directories: ‘/Users/kalpesh/sites/magento/app/etc’  
[Progress: 484 / 485]  
Write installation date…  
[Progress: 485 / 485]  
[SUCCESS]: Magento installation complete.  
[SUCCESS]: Magento Admin URI: /admin  
Nothing to import.  
Install sample data? [y]: y  
bin/magento > ./composer.json has been updated  
bin/magento > Loading composer repositories with package information  
bin/magento >  
Installation failed, reverting ./composer.json to its original content.  
bin/magento >  
bin/magento > bin/magento >  
bin/magento > [Composer\\Downloader\\TransportException]  
The ‘https://repo.magento.com/packages.json’ URL required authentication.  
bin/magento > You must be using the interactive console to authenticate

bin/magento > require [–dev] [–prefer-source] [–prefer-dist] [–no-progress] [–no-suggest] [–no-update] [–no-scripts] [–update-no-dev] [–update-with-dependencies] [–ignore-platform-reqs] [–prefer-stable] [–prefer-lowest] [–sort-packages] [-o|–optimize-autoloader] [-a|–classmap-authoritative] [–apcu-autoloader] [–] [<packages>]…

bin/magento > There is an error during sample data deployment. Composer file will be reverted.  
bin/magento > Cache cleared successfully  
File system cleanup:  
bin/magento > /Users/kalpesh/sites/magento/generated/code/Composer  
bin/magento > /Users/kalpesh/sites/magento/generated/code/Magento  
/Users/kalpesh/sites/magento/generated/code/Symfony  
Updating modules:  
bin/magento > Schema creation/updates:  
bin/magento > Module ‘Magento_Store’:  
bin/magento > Module ‘Magento_Directory’:  
bin/magento > Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Config’:  
Module ‘Magento_Backend’:  
bin/magento > Module ‘Magento_Theme’:  
Module ‘Magento_Eav’:  
bin/magento > Module ‘Magento_Backup’:  
bin/magento > Module ‘Magento_Customer’:  
Module ‘Magento_AdminNotification’:  
bin/magento > Module ‘Magento_BundleImportExport’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
bin/magento > Module ‘Magento_Cms’:  
bin/magento > Module ‘Magento_Security’:  
Module ‘Magento_CatalogImportExport’:  
bin/magento > Module ‘Magento_Rule’:  
Module ‘Magento_Cron’:  
Module ‘Magento_Catalog’:  
bin/magento > Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
bin/magento > Module ‘Magento_Widget’:  
bin/magento > Module ‘Magento_Quote’:  
bin/magento > Module ‘Magento_SalesSequence’:  
Module ‘Magento_Payment’:  
bin/magento > Module ‘Magento_CmsUrlRewrite’:  
bin/magento > Module ‘Magento_User’:  
bin/magento > Module ‘Magento_ConfigurableImportExport’:  
bin/magento > Module ‘Magento_Msrp’:  
bin/magento > Module ‘Magento_CatalogInventory’:  
bin/magento > Module ‘Magento_Contact’:  
bin/magento > Module ‘Magento_Cookie’:  
bin/magento > Module ‘Magento_Newsletter’:  
bin/magento > Module ‘Magento_CurrencySymbol’:  
bin/magento > Module ‘Magento_Sales’:  
bin/magento > Module ‘Magento_Integration’:  
bin/magento > Module ‘Magento_CustomerImportExport’:  
bin/magento > Module ‘Magento_Deploy’:  
bin/magento > Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
bin/magento > Module ‘Magento_Authorization’:  
bin/magento > Module ‘Magento_Downloadable’:  
bin/magento > Module ‘Magento_ImportExport’:  
bin/magento > Module ‘Magento_Bundle’:  
Module ‘Magento_Email’:  
bin/magento > Module ‘Magento_EncryptionKey’:  
bin/magento > Module ‘Magento_Fedex’:  
bin/magento > Module ‘Magento_GiftMessage’:  
bin/magento > Module ‘Magento_Checkout’:  
bin/magento > Module ‘Magento_GoogleAnalytics’:  
bin/magento > Module ‘Magento_Ui’:  
bin/magento > Module ‘Magento_GroupedImportExport’:  
bin/magento > Module ‘Magento_GroupedProduct’:  
bin/magento > Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_CatalogRule’:  
bin/magento > Module ‘Magento_InstantPurchase’:  
bin/magento > Module ‘Magento_Analytics’:  
bin/magento > Module ‘Magento_LayeredNavigation’:  
bin/magento > Module ‘Magento_Marketplace’:  
bin/magento > Module ‘Magento_MediaStorage’:  
bin/magento > Module ‘Magento_ConfigurableProduct’:  
bin/magento > Module ‘Magento_Multishipping’:  
bin/magento > Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Reports’:  
bin/magento > Module ‘Magento_OfflinePayments’:  
bin/magento > Module ‘Magento_SalesRule’:  
bin/magento > Module ‘Magento_PageCache’:  
bin/magento > Module ‘Magento_Vault’:  
bin/magento > Module ‘Magento_Paypal’:  
bin/magento > Module ‘Magento_Persistent’:  
bin/magento > Module ‘Magento_ProductAlert’:  
bin/magento > Module ‘Magento_ProductVideo’:  
bin/magento > Module ‘Magento_CheckoutAgreements’:  
bin/magento > Module ‘Magento_QuoteAnalytics’:  
bin/magento > Module ‘Magento_ReleaseNotification’:  
bin/magento > Module ‘Magento_Review’:  
bin/magento > Module ‘Magento_RequireJs’:  
bin/magento > Module ‘Magento_Shipping’:  
bin/magento > Module ‘Magento_ReviewAnalytics’:  
bin/magento > Module ‘Magento_Robots’:  
bin/magento > Module ‘Magento_Rss’:  
bin/magento > Module ‘Magento_CatalogRuleConfigurable’:  
bin/magento > Module ‘Magento_Captcha’:  
bin/magento > Module ‘Magento_SalesAnalytics’:  
bin/magento > Module ‘Magento_SalesInventory’:  
bin/magento > Module ‘Magento_OfflineShipping’:  
bin/magento > Module ‘Magento_ConfigurableProductSales’:  
bin/magento > Module ‘Magento_UrlRewrite’:  
bin/magento > Module ‘Magento_CatalogSearch’:  
bin/magento > Module ‘Magento_CustomerAnalytics’:  
bin/magento > Module ‘Magento_SendFriend’:  
bin/magento > Module ‘Magento_Wishlist’:  
Module ‘Magento_Signifyd’:  
bin/magento > Module ‘Magento_Sitemap’:  
bin/magento > Module ‘Magento_Authorizenet’:  
bin/magento > Module ‘Magento_Swagger’:  
bin/magento > Module ‘Magento_Swatches’:  
bin/magento > Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_Tax’:  
Module ‘Magento_TaxImportExport’:  
bin/magento > Module ‘Magento_GoogleAdwords’:  
bin/magento > Module ‘Magento_Translation’:  
bin/magento > Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
bin/magento > Module ‘Magento_SampleData’:  
bin/magento > Module ‘Magento_CatalogAnalytics’:  
bin/magento > Module ‘Magento_Usps’:  
bin/magento > Module ‘Magento_Variable’:  
bin/magento > Module ‘Magento_Braintree’:  
bin/magento > Module ‘Magento_Version’:  
bin/magento > Module ‘Magento_Webapi’:  
bin/magento > Module ‘Magento_WebapiSecurity’:  
bin/magento > Module ‘Magento_Weee’:  
bin/magento > Module ‘Magento_CatalogWidget’:  
bin/magento > Module ‘Dotdigitalgroup_Email’:  
bin/magento > Module ‘Magento_WishlistAnalytics’:  
bin/magento > Module ‘Shopial_Facebook’:  
bin/magento > Module ‘Temando_Shipping’:  
bin/magento > Schema post-updates:  
bin/magento > Module ‘Magento_Store’:  
bin/magento > Module ‘Magento_Directory’:  
bin/magento > Module ‘Magento_AdvancedPricingImportExport’:  
bin/magento > Module ‘Magento_Config’:  
bin/magento > Module ‘Magento_Backend’:  
bin/magento > Module ‘Magento_Theme’:  
bin/magento > Module ‘Magento_Eav’:  
bin/magento > Module ‘Magento_Backup’:  
bin/magento > Module ‘Magento_Customer’:  
bin/magento > Module ‘Magento_AdminNotification’:  
bin/magento > Module ‘Magento_BundleImportExport’:  
bin/magento > Module ‘Magento_CacheInvalidate’:  
bin/magento > Module ‘Magento_Indexer’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Cms’:  
bin/magento > Module ‘Magento_Security’:  
bin/magento > Module ‘Magento_CatalogImportExport’:  
bin/magento > Module ‘Magento_Rule’:  
bin/magento > Module ‘Magento_Cron’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Catalog’:  
bin/magento > Running schema recurring…bin/magento >  
Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Widget’:  
bin/magento > Module ‘Magento_Quote’:  
bin/magento > Module ‘Magento_SalesSequence’:  
Module ‘Magento_Payment’:  
bin/magento > Module ‘Magento_CmsUrlRewrite’:  
bin/magento > Module ‘Magento_User’:  
bin/magento > Module ‘Magento_ConfigurableImportExport’:  
bin/magento > Module ‘Magento_Msrp’:  
bin/magento > Module ‘Magento_CatalogInventory’:  
bin/magento > Running schema recurring…bin/magento >  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Integration’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_CustomerImportExport’:  
bin/magento > Module ‘Magento_Deploy’:  
bin/magento > Module ‘Magento_Developer’:  
bin/magento > Module ‘Magento_Dhl’:  
bin/magento > Module ‘Magento_Authorization’:  
bin/magento > Module ‘Magento_Downloadable’:  
bin/magento > Module ‘Magento_ImportExport’:  
bin/magento > Module ‘Magento_Bundle’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Email’:  
bin/magento > Module ‘Magento_EncryptionKey’:  
bin/magento > Module ‘Magento_Fedex’:  
bin/magento > Module ‘Magento_GiftMessage’:  
bin/magento > Module ‘Magento_Checkout’:  
bin/magento > Module ‘Magento_GoogleAnalytics’:  
bin/magento > Module ‘Magento_Ui’:  
bin/magento > Module ‘Magento_GroupedImportExport’:  
bin/magento > Module ‘Magento_GroupedProduct’:  
bin/magento > Module ‘Magento_DownloadableImportExport’:  
bin/magento > Module ‘Magento_CatalogRule’:  
bin/magento > Module ‘Magento_InstantPurchase’:  
bin/magento > Module ‘Magento_Analytics’:  
bin/magento > Module ‘Magento_LayeredNavigation’:  
bin/magento > Module ‘Magento_Marketplace’:  
bin/magento > Module ‘Magento_MediaStorage’:  
bin/magento > Module ‘Magento_ConfigurableProduct’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Multishipping’:  
bin/magento > Module ‘Magento_NewRelicReporting’:  
bin/magento > Module ‘Magento_Reports’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_OfflinePayments’:  
bin/magento > Module ‘Magento_SalesRule’:  
bin/magento > Module ‘Magento_PageCache’:  
bin/magento > Module ‘Magento_Vault’:  
bin/magento > Module ‘Magento_Paypal’:  
bin/magento > Module ‘Magento_Persistent’:  
bin/magento > Module ‘Magento_ProductAlert’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_ProductVideo’:  
bin/magento > Module ‘Magento_CheckoutAgreements’:  
bin/magento > Module ‘Magento_QuoteAnalytics’:  
bin/magento > Module ‘Magento_ReleaseNotification’:  
bin/magento > Module ‘Magento_Review’:  
bin/magento > Module ‘Magento_RequireJs’:  
bin/magento > Module ‘Magento_Shipping’:  
bin/magento > Module ‘Magento_ReviewAnalytics’:  
bin/magento > Module ‘Magento_Robots’:  
bin/magento > Module ‘Magento_Rss’:  
bin/magento > Module ‘Magento_CatalogRuleConfigurable’:  
bin/magento > Module ‘Magento_Captcha’:  
bin/magento > Module ‘Magento_SalesAnalytics’:  
bin/magento > Module ‘Magento_SalesInventory’:  
bin/magento > Module ‘Magento_OfflineShipping’:  
bin/magento > Module ‘Magento_ConfigurableProductSales’:  
bin/magento > Module ‘Magento_UrlRewrite’:  
bin/magento > Module ‘Magento_CatalogSearch’:  
bin/magento > Module ‘Magento_CustomerAnalytics’:  
bin/magento > Module ‘Magento_SendFriend’:  
bin/magento > Module ‘Magento_Wishlist’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_Signifyd’:  
bin/magento > Module ‘Magento_Sitemap’:  
bin/magento > Module ‘Magento_Authorizenet’:  
bin/magento > Module ‘Magento_Swagger’:  
bin/magento > Module ‘Magento_Swatches’:  
bin/magento > Module ‘Magento_SwatchesLayeredNavigation’:  
bin/magento > Module ‘Magento_Tax’:  
bin/magento > Module ‘Magento_TaxImportExport’:  
bin/magento > Module ‘Magento_GoogleAdwords’:  
bin/magento > Module ‘Magento_Translation’:  
bin/magento > Module ‘Magento_GoogleOptimizer’:  
bin/magento > Module ‘Magento_Ups’:  
bin/magento > Module ‘Magento_SampleData’:  
bin/magento > Module ‘Magento_CatalogAnalytics’:  
bin/magento > Module ‘Magento_Usps’:  
bin/magento > Module ‘Magento_Variable’:  
bin/magento > Module ‘Magento_Braintree’:  
bin/magento > Module ‘Magento_Version’:  
bin/magento > Module ‘Magento_Webapi’:  
bin/magento > Module ‘Magento_WebapiSecurity’:  
bin/magento > Module ‘Magento_Weee’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_CatalogWidget’:  
bin/magento > Module ‘Dotdigitalgroup_Email’:  
bin/magento > Running schema recurring…bin/magento >  
bin/magento > Module ‘Magento_WishlistAnalytics’:  
bin/magento > Module ‘Shopial_Facebook’:  
bin/magento > Module ‘Temando_Shipping’:  
bin/magento > Data install/update:  
bin/magento > Module ‘Magento_Store’:  
bin/magento > Module ‘Magento_Directory’:  
Module ‘Magento_AdvancedPricingImportExport’:  
bin/magento > Module ‘Magento_Config’:  
bin/magento > Module ‘Magento_Backend’:  
bin/magento > Module ‘Magento_Theme’:  
bin/magento > Module ‘Magento_Eav’:  
bin/magento > Module ‘Magento_Backup’:  
bin/magento > Module ‘Magento_Customer’:  
bin/magento > Module ‘Magento_AdminNotification’:  
bin/magento > Module ‘Magento_BundleImportExport’:  
bin/magento > Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
bin/magento > Module ‘Magento_Cms’:  
bin/magento > Module ‘Magento_Security’:  
bin/magento > Module ‘Magento_CatalogImportExport’:  
bin/magento > Module ‘Magento_Rule’:  
bin/magento > Module ‘Magento_Cron’:  
bin/magento > Module ‘Magento_Catalog’:  
bin/magento > Module ‘Magento_Search’:  
bin/magento > Module ‘Magento_CatalogUrlRewrite’:  
bin/magento > Module ‘Magento_Widget’:  
bin/magento > Module ‘Magento_Quote’:  
bin/magento > Module ‘Magento_SalesSequence’:  
bin/magento > Module ‘Magento_Payment’:  
bin/magento > Module ‘Magento_CmsUrlRewrite’:  
bin/magento > Module ‘Magento_User’:  
bin/magento > Module ‘Magento_ConfigurableImportExport’:  
bin/magento > Module ‘Magento_Msrp’:  
bin/magento > Module ‘Magento_CatalogInventory’:  
Module ‘Magento_Contact’:  
bin/magento > Module ‘Magento_Cookie’:  
bin/magento > Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
bin/magento > Module ‘Magento_Integration’:  
bin/magento > Module ‘Magento_CustomerImportExport’:  
bin/magento > Module ‘Magento_Deploy’:  
bin/magento > Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
bin/magento > Module ‘Magento_Authorization’:  
bin/magento > Module ‘Magento_Downloadable’:  
bin/magento > Module ‘Magento_ImportExport’:  
bin/magento > Module ‘Magento_Bundle’:  
Module ‘Magento_Email’:  
bin/magento > Module ‘Magento_EncryptionKey’:  
bin/magento > Module ‘Magento_Fedex’:  
bin/magento > Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
bin/magento > Module ‘Magento_GoogleAnalytics’:  
bin/magento > Module ‘Magento_Ui’:  
bin/magento > Module ‘Magento_GroupedImportExport’:  
bin/magento > Module ‘Magento_GroupedProduct’:  
bin/magento > Module ‘Magento_DownloadableImportExport’:  
bin/magento > Module ‘Magento_CatalogRule’:  
bin/magento > Module ‘Magento_InstantPurchase’:  
bin/magento > Module ‘Magento_Analytics’:  
bin/magento > Module ‘Magento_LayeredNavigation’:  
bin/magento > Module ‘Magento_Marketplace’:  
bin/magento > Module ‘Magento_MediaStorage’:  
bin/magento > Module ‘Magento_ConfigurableProduct’:  
bin/magento > Module ‘Magento_Multishipping’:  
bin/magento > Module ‘Magento_NewRelicReporting’:  
bin/magento > Module ‘Magento_Reports’:  
bin/magento > Module ‘Magento_OfflinePayments’:  
bin/magento > Module ‘Magento_SalesRule’:  
bin/magento > Module ‘Magento_PageCache’:  
bin/magento > Module ‘Magento_Vault’:  
bin/magento > Module ‘Magento_Paypal’:  
bin/magento > Module ‘Magento_Persistent’:  
bin/magento > Module ‘Magento_ProductAlert’:  
bin/magento > Module ‘Magento_ProductVideo’:  
bin/magento > Module ‘Magento_CheckoutAgreements’:  
bin/magento > Module ‘Magento_QuoteAnalytics’:  
bin/magento > Module ‘Magento_ReleaseNotification’:  
bin/magento > Module ‘Magento_Review’:  
bin/magento > Module ‘Magento_RequireJs’:  
bin/magento > Module ‘Magento_Shipping’:  
bin/magento > Module ‘Magento_ReviewAnalytics’:  
bin/magento > Module ‘Magento_Robots’:  
bin/magento > Module ‘Magento_Rss’:  
bin/magento > Module ‘Magento_CatalogRuleConfigurable’:  
bin/magento > Module ‘Magento_Captcha’:  
bin/magento > Module ‘Magento_SalesAnalytics’:  
bin/magento > Module ‘Magento_SalesInventory’:  
bin/magento > Module ‘Magento_OfflineShipping’:  
bin/magento > Module ‘Magento_ConfigurableProductSales’:  
bin/magento > Module ‘Magento_UrlRewrite’:  
bin/magento > Module ‘Magento_CatalogSearch’:  
bin/magento > Module ‘Magento_CustomerAnalytics’:  
bin/magento > Module ‘Magento_SendFriend’:  
bin/magento > Module ‘Magento_Wishlist’:  
bin/magento > Module ‘Magento_Signifyd’:  
bin/magento > Module ‘Magento_Sitemap’:  
bin/magento > Module ‘Magento_Authorizenet’:  
bin/magento > Module ‘Magento_Swagger’:  
bin/magento > Module ‘Magento_Swatches’:  
bin/magento > Module ‘Magento_SwatchesLayeredNavigation’:  
bin/magento > Module ‘Magento_Tax’:  
bin/magento > Module ‘Magento_TaxImportExport’:  
bin/magento > Module ‘Magento_GoogleAdwords’:  
bin/magento > Module ‘Magento_Translation’:  
bin/magento > Module ‘Magento_GoogleOptimizer’:  
bin/magento > Module ‘Magento_Ups’:  
bin/magento > Module ‘Magento_SampleData’:  
bin/magento > Module ‘Magento_CatalogAnalytics’:  
bin/magento > Module ‘Magento_Usps’:  
bin/magento > Module ‘Magento_Variable’:  
bin/magento > Module ‘Magento_Braintree’:  
bin/magento > Module ‘Magento_Version’:  
bin/magento > Module ‘Magento_Webapi’:  
bin/magento > Module ‘Magento_WebapiSecurity’:  
bin/magento > Module ‘Magento_Weee’:  
bin/magento > Module ‘Magento_CatalogWidget’:  
bin/magento > Module ‘Dotdigitalgroup_Email’:  
bin/magento > Module ‘Magento_WishlistAnalytics’:  
bin/magento > Module ‘Shopial_Facebook’:  
bin/magento > Module ‘Temando_Shipping’:  
bin/magento > Data post-updates:  
bin/magento > Module ‘Magento_Store’:  
bin/magento > Module ‘Magento_Directory’:  
bin/magento > Module ‘Magento_AdvancedPricingImportExport’:  
bin/magento > Module ‘Magento_Config’:  
bin/magento > Module ‘Magento_Backend’:  
bin/magento > Module ‘Magento_Theme’:  
bin/magento > Running data recurring…bin/magento >  
Module ‘Magento_Eav’:  
bin/magento > Module ‘Magento_Backup’:  
bin/magento > Module ‘Magento_Customer’:  
bin/magento > Module ‘Magento_AdminNotification’:  
bin/magento > Module ‘Magento_BundleImportExport’:  
bin/magento > Module ‘Magento_CacheInvalidate’:  
bin/magento > Module ‘Magento_Indexer’:  
bin/magento > Running data recurring…bin/magento >  
bin/magento > Module ‘Magento_Cms’:  
bin/magento > Module ‘Magento_Security’:  
bin/magento > Module ‘Magento_CatalogImportExport’:  
bin/magento > Module ‘Magento_Rule’:  
bin/magento > Module ‘Magento_Cron’:  
bin/magento > Module ‘Magento_Catalog’:  
bin/magento > Module ‘Magento_Search’:  
bin/magento > Module ‘Magento_CatalogUrlRewrite’:  
bin/magento > Module ‘Magento_Widget’:  
bin/magento > Module ‘Magento_Quote’:  
bin/magento > Module ‘Magento_SalesSequence’:  
bin/magento > Running data recurring…bin/magento >  
bin/magento > Module ‘Magento_Payment’:  
bin/magento > Module ‘Magento_CmsUrlRewrite’:  
bin/magento > Module ‘Magento_User’:  
bin/magento > Module ‘Magento_ConfigurableImportExport’:  
bin/magento > Module ‘Magento_Msrp’:  
bin/magento > Module ‘Magento_CatalogInventory’:  
bin/magento > Module ‘Magento_Contact’:  
bin/magento > Module ‘Magento_Cookie’:  
bin/magento > Module ‘Magento_Newsletter’:  
bin/magento > Module ‘Magento_CurrencySymbol’:  
bin/magento > Module ‘Magento_Sales’:  
bin/magento > Module ‘Magento_Integration’:  
bin/magento > Module ‘Magento_CustomerImportExport’:  
bin/magento > Module ‘Magento_Deploy’:  
bin/magento > Module ‘Magento_Developer’:  
bin/magento > Module ‘Magento_Dhl’:  
bin/magento > Module ‘Magento_Authorization’:  
bin/magento > Module ‘Magento_Downloadable’:  
bin/magento > Module ‘Magento_ImportExport’:  
bin/magento > Module ‘Magento_Bundle’:  
bin/magento > Module ‘Magento_Email’:  
bin/magento > Module ‘Magento_EncryptionKey’:  
bin/magento > Module ‘Magento_Fedex’:  
bin/magento > Module ‘Magento_GiftMessage’:  
bin/magento > Module ‘Magento_Checkout’:  
bin/magento > Module ‘Magento_GoogleAnalytics’:  
bin/magento > Module ‘Magento_Ui’:  
bin/magento > Module ‘Magento_GroupedImportExport’:  
bin/magento > Module ‘Magento_GroupedProduct’:  
bin/magento > Module ‘Magento_DownloadableImportExport’:  
bin/magento > Module ‘Magento_CatalogRule’:  
bin/magento > Module ‘Magento_InstantPurchase’:  
bin/magento > Module ‘Magento_Analytics’:  
bin/magento > Module ‘Magento_LayeredNavigation’:  
bin/magento > Module ‘Magento_Marketplace’:  
bin/magento > Module ‘Magento_MediaStorage’:  
bin/magento > Module ‘Magento_ConfigurableProduct’:  
bin/magento > Module ‘Magento_Multishipping’:  
bin/magento > Module ‘Magento_NewRelicReporting’:  
bin/magento > Module ‘Magento_Reports’:  
bin/magento > Module ‘Magento_OfflinePayments’:  
bin/magento > Module ‘Magento_SalesRule’:  
bin/magento > Module ‘Magento_PageCache’:  
bin/magento > Module ‘Magento_Vault’:  
bin/magento > Module ‘Magento_Paypal’:  
bin/magento > Module ‘Magento_Persistent’:  
bin/magento > Module ‘Magento_ProductAlert’:  
bin/magento > Module ‘Magento_ProductVideo’:  
bin/magento > Module ‘Magento_CheckoutAgreements’:  
bin/magento > Module ‘Magento_QuoteAnalytics’:  
bin/magento > Module ‘Magento_ReleaseNotification’:  
bin/magento > Module ‘Magento_Review’:  
bin/magento > Module ‘Magento_RequireJs’:  
bin/magento > Module ‘Magento_Shipping’:  
bin/magento > Module ‘Magento_ReviewAnalytics’:  
bin/magento > Module ‘Magento_Robots’:  
bin/magento > Module ‘Magento_Rss’:  
bin/magento > Module ‘Magento_CatalogRuleConfigurable’:  
bin/magento > Module ‘Magento_Captcha’:  
bin/magento > Module ‘Magento_SalesAnalytics’:  
bin/magento > Module ‘Magento_SalesInventory’:  
bin/magento > Module ‘Magento_OfflineShipping’:  
bin/magento > Module ‘Magento_ConfigurableProductSales’:  
bin/magento > Module ‘Magento_UrlRewrite’:  
bin/magento > Module ‘Magento_CatalogSearch’:  
bin/magento > Module ‘Magento_CustomerAnalytics’:  
bin/magento > Module ‘Magento_SendFriend’:  
bin/magento > Module ‘Magento_Wishlist’:  
bin/magento > Module ‘Magento_Signifyd’:  
bin/magento > Module ‘Magento_Sitemap’:  
bin/magento > Module ‘Magento_Authorizenet’:  
bin/magento > Module ‘Magento_Swagger’:  
bin/magento > Module ‘Magento_Swatches’:  
bin/magento > Module ‘Magento_SwatchesLayeredNavigation’:  
bin/magento > Module ‘Magento_Tax’:  
bin/magento > Module ‘Magento_TaxImportExport’:  
bin/magento > Module ‘Magento_GoogleAdwords’:  
bin/magento > Module ‘Magento_Translation’:  
bin/magento > Module ‘Magento_GoogleOptimizer’:  
bin/magento > Module ‘Magento_Ups’:  
bin/magento > Module ‘Magento_SampleData’:  
bin/magento > Module ‘Magento_CatalogAnalytics’:  
bin/magento > Module ‘Magento_Usps’:  
bin/magento > Module ‘Magento_Variable’:  
bin/magento > Module ‘Magento_Braintree’:  
bin/magento > Module ‘Magento_Version’:  
bin/magento > Module ‘Magento_Webapi’:  
bin/magento > Module ‘Magento_WebapiSecurity’:  
bin/magento > Module ‘Magento_Weee’:  
bin/magento > Module ‘Magento_CatalogWidget’:  
bin/magento > Module ‘Dotdigitalgroup_Email’:  
bin/magento > Module ‘Magento_WishlistAnalytics’:  
bin/magento > Module ‘Shopial_Facebook’:  
bin/magento > Module ‘Temando_Shipping’:  
bin/magento > Nothing to import.  
Reindex all after installation  
Design Config Grid index has been rebuilt successfully in 00:00:01  
Customer Grid index has been rebuilt successfully in 00:00:03  
Category Products index has been rebuilt successfully in 00:00:01  
Product Categories index has been rebuilt successfully in 00:00:00  
Product Price index has been rebuilt successfully in 00:00:00  
Product EAV index has been rebuilt successfully in 00:00:00  
Stock index has been rebuilt successfully in 00:00:00  
Catalog Rule Product index has been rebuilt successfully in 00:00:02  
Catalog Product Rule index has been rebuilt successfully in 00:00:00  
Catalog Search index has been rebuilt successfully in 00:00:13  
Successfully installed magento{{< /highlight >}}

At this point, your Magento 2.2.2 is installed and can be accessed at http://magento.test or whatever base URL you provided during installation steps.

You can access the admin panel at http://magento.test/admin and credentials would be admin / password123

10.) Now that Magento 2.2.2 is installed, let’s upgrade it to Magento 2.2.3

<span class="s1">cd magento</span>

<span class="s1">composer require magento/product-community-edition 2.2.3 –no-update</span>

<span class="s1">composer update</span>

<span class="s1">bin/magento setup:upgrade</span>

{{< highlight http >}} 

Kalpeshs-MBP:magento kalpesh$ composer require magento/product-community-edition 2.2.3 –no-update  
./composer.json has been updated  
Kalpeshs-MBP:magento kalpesh$ composer update  
Loading composer repositories with package information  
Updating dependencies (including require-dev)  
Package operations: 47 installs, 30 updates, 0 removals  
– Updating tedivm/jshrink (v1.2.0 => v1.3.0): Downloading (100%)  
– Updating magento/framework (101.0.2 => 101.0.3): Downloading (100%)  
– Updating magento/module-config (101.0.2 => 101.0.3): Downloading (100%)  
– Updating magento/module-variable (100.2.1 => 100.2.2): Downloading (100%)  
– Updating magento/module-ui (101.0.2 => 101.0.3): Downloading (100%)  
– Updating magento/module-backend (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-eav (101.0.1 => 101.0.2): Downloading (100%)  
– Updating magento/module-catalog (102.0.2 => 102.0.3): Downloading (100%)  
– Updating magento/module-theme (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-customer (101.0.2 => 101.0.3): Downloading (100%)  
– Updating magento/module-tax (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-reports (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-shipping (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-directory (100.2.1 => 100.2.2): Downloading (100%)  
– Updating magento/module-checkout (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-cms (102.0.2 => 102.0.3): Downloading (100%)  
– Updating magento/module-downloadable (100.2.1 => 100.2.2): Downloading (100%)  
– Updating magento/module-newsletter (100.2.1 => 100.2.2): Downloading (100%)  
– Updating magento/module-review (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-import-export (100.2.2 => 100.2.3): Downloading (100%)  
– Updating magento/module-backup (100.2.1 => 100.2.2): Downloading (100%)  
– Updating magento/module-usps (100.2.0 => 100.2.1): Downloading (100%)  
– Updating magento/module-configurable-product (100.2.2 => 100.2.3): Downloading (100%)  
– Updating braintree/braintree_php (3.25.0 => 3.27.0): Downloading (100%)  
– Updating magento/module-braintree (100.2.2 => 100.2.3): Downloading (100%)  
– Updating ramsey/uuid (3.7.1 => 3.7.3): Downloading (100%)  
– Updating tubalmartin/cssmin (v4.1.0 => v4.1.1): Downloading (100%)  
– Updating colinmollenhour/cache-backend-redis (1.10.2 => 1.10.4): Downloading (100%)  
– Updating magento/magento2-base (2.2.2 => 2.2.3): Downloading (100%)  
– Installing squizlabs/php_codesniffer (3.1.1): Downloading (100%)  
– Installing lusitanian/oauth (v0.8.10): Downloading (100%)  
– Installing theseer/fdomdocument (1.6.6): Downloading (100%)  
– Installing sebastian/version (2.0.1): Downloading (100%)  
– Installing sebastian/resource-operations (1.0.0): Downloading (100%)  
– Installing sebastian/recursion-context (3.0.0): Downloading (100%)  
– Installing sebastian/object-reflector (1.1.1): Downloading (100%)  
– Installing sebastian/object-enumerator (3.0.3): Downloading (100%)  
– Installing sebastian/global-state (2.0.0): Downloading (100%)  
– Installing sebastian/exporter (3.1.0): Downloading (100%)  
– Installing sebastian/environment (3.1.0): Downloading (100%)  
– Installing sebastian/diff (1.4.3): Downloading (100%)  
– Installing sebastian/comparator (2.0.0): Downloading (100%)  
– Installing doctrine/instantiator (1.1.0): Downloading (100%)  
– Installing phpunit/php-text-template (1.2.1): Downloading (100%)  
– Installing phpunit/phpunit-mock-objects (4.0.4): Downloading (100%)  
– Installing phpunit/php-timer (1.0.9): Downloading (100%)  
– Installing phpunit/php-file-iterator (1.4.5): Downloading (100%)  
– Installing theseer/tokenizer (1.1.0): Downloading (100%)  
– Installing sebastian/code-unit-reverse-lookup (1.0.1): Downloading (100%)  
– Installing phpunit/php-token-stream (2.0.2): Downloading (100%)  
– Installing phpunit/php-code-coverage (5.3.0): Downloading (100%)  
– Installing webmozart/assert (1.3.0): Downloading (100%)  
– Installing phpdocumentor/reflection-common (1.0.1): Downloading (100%)  
– Installing phpdocumentor/type-resolver (0.4.0): Downloading (100%)  
– Installing phpdocumentor/reflection-docblock (4.3.0): Downloading (100%)  
– Installing phpspec/prophecy (1.7.5): Downloading (100%)  
– Installing phar-io/version (1.0.1): Downloading (100%)  
– Installing phar-io/manifest (1.0.1): Downloading (100%)  
– Installing myclabs/deep-copy (1.7.0): Downloading (100%)  
– Installing phpunit/phpunit (6.2.4): Downloading (100%)  
– Installing sebastian/finder-facade (1.2.2): Downloading (100%)  
– Installing sebastian/phpcpd (2.0.4): Downloading (100%)  
– Installing symfony/config (v3.4.6): Downloading (100%)  
– Installing symfony/dependency-injection (v3.4.6): Downloading (100%)  
– Installing pdepend/pdepend (2.5.0): Downloading (100%)  
– Installing phpmd/phpmd (2.6.0): Downloading (100%)  
– Installing symfony/stopwatch (v4.0.6): Downloading (100%)  
– Installing symfony/polyfill-php72 (v1.7.0): Downloading (100%)  
– Installing symfony/polyfill-php70 (v1.7.0): Downloading (100%)  
– Installing ircmaxell/password-compat (v1.0.4): Downloading (100%)  
– Installing symfony/polyfill-php55 (v1.7.0): Downloading (100%)  
– Installing symfony/polyfill-php54 (v1.7.0): Downloading (100%)  
– Installing symfony/options-resolver (v4.0.6): Downloading (100%)  
– Installing doctrine/lexer (v1.0.1): Downloading (100%)  
– Installing doctrine/annotations (v1.6.0): Downloading (100%)  
– Installing friendsofphp/php-cs-fixer (v2.2.18): Downloading (100%)  
lusitanian/oauth suggests installing symfony/http-foundation (Allows using the Symfony Session storage backend.)  
lusitanian/oauth suggests installing predis/predis (Allows using the Redis storage backend.)  
sebastian/global-state suggests installing ext-uopz (*)  
phpunit/php-code-coverage suggests installing ext-xdebug (^2.5.5)  
phpunit/phpunit suggests installing phpunit/php-invoker (^1.1)  
phpunit/phpunit suggests installing ext-xdebug (*)  
symfony/config suggests installing symfony/yaml (To use the yaml reference dumper)  
symfony/dependency-injection suggests installing symfony/expression-language (For using expressions in service container configuration)  
symfony/dependency-injection suggests installing symfony/proxy-manager-bridge (Generate service proxies to lazy load them)  
symfony/dependency-injection suggests installing symfony/yaml ()  
Package sjparkinson/static-review is abandoned, you should avoid using it. Use phpro/grumphp instead.  
Writing lock file  
Generating autoload files

Kalpeshs-MBP:magento kalpesh$ rm -rf var/cache/* var/page_cache/* generated/*  
Kalpeshs-MBP:magento kalpesh$ bin/magento setup:upgrade  
Cache cleared successfully  
File system cleanup:  
/Users/kalpesh/sites/magento/generated/code/Composer  
/Users/kalpesh/sites/magento/generated/code/Magento  
/Users/kalpesh/sites/magento/generated/code/Symfony  
/Users/kalpesh/sites/magento/pub/static/adminhtml  
/Users/kalpesh/sites/magento/pub/static/deployed_version.txt  
/Users/kalpesh/sites/magento/pub/static/frontend  
/Users/kalpesh/sites/magento/var/view_preprocessed/pub  
Updating modules:  
Schema creation/updates:  
Module ‘Magento_Store’:  
Module ‘Magento_Directory’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Config’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Theme’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Customer’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Module ‘Magento_Cms’:  
Module ‘Magento_Security’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Rule’:  
Module ‘Magento_Cron’:  
Module ‘Magento_Catalog’:  
Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_Quote’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_Payment’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_User’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_CatalogInventory’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Integration’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_Bundle’:  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_InstantPurchase’:  
Module ‘Magento_Analytics’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Reports’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_QuoteAnalytics’:  
Module ‘Magento_ReleaseNotification’:  
Module ‘Magento_Review’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_ReviewAnalytics’:  
Module ‘Magento_Robots’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_SalesAnalytics’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_ConfigurableProductSales’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_CustomerAnalytics’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_Signifyd’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_Tax’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CatalogAnalytics’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_Weee’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Dotdigitalgroup_Email’:  
Module ‘Magento_WishlistAnalytics’:  
Module ‘Shopial_Facebook’:  
Module ‘Temando_Shipping’:  
Schema post-updates:  
Module ‘Magento_Store’:  
Module ‘Magento_Directory’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Config’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Theme’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Customer’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Running schema recurring…  
Module ‘Magento_Cms’:  
Module ‘Magento_Security’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Rule’:  
Module ‘Magento_Cron’:  
Running schema recurring…  
Module ‘Magento_Catalog’:  
Running schema recurring…  
Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
Running schema recurring…  
Module ‘Magento_Widget’:  
Module ‘Magento_Quote’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_Payment’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_User’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_CatalogInventory’:  
Running schema recurring…  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Integration’:  
Running schema recurring…  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_Bundle’:  
Running schema recurring…  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_InstantPurchase’:  
Module ‘Magento_Analytics’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Running schema recurring…  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Reports’:  
Running schema recurring…  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Running schema recurring…  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_QuoteAnalytics’:  
Module ‘Magento_ReleaseNotification’:  
Module ‘Magento_Review’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_ReviewAnalytics’:  
Module ‘Magento_Robots’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_SalesAnalytics’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_ConfigurableProductSales’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_CustomerAnalytics’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Wishlist’:  
Running schema recurring…  
Module ‘Magento_Signifyd’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_Tax’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CatalogAnalytics’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_Weee’:  
Running schema recurring…  
Module ‘Magento_CatalogWidget’:  
Module ‘Dotdigitalgroup_Email’:  
Running schema recurring…  
Module ‘Magento_WishlistAnalytics’:  
Module ‘Shopial_Facebook’:  
Module ‘Temando_Shipping’:  
Data install/update:  
Module ‘Magento_Store’:  
Module ‘Magento_Directory’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Config’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Theme’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Customer’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Module ‘Magento_Cms’:  
Module ‘Magento_Security’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Rule’:  
Module ‘Magento_Cron’:  
Module ‘Magento_Catalog’:  
Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_Quote’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_Payment’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_User’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_CatalogInventory’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Integration’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_Bundle’:  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_InstantPurchase’:  
Module ‘Magento_Analytics’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Reports’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_QuoteAnalytics’:  
Module ‘Magento_ReleaseNotification’:  
Module ‘Magento_Review’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_ReviewAnalytics’:  
Module ‘Magento_Robots’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_SalesAnalytics’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_ConfigurableProductSales’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_CustomerAnalytics’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_Signifyd’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_Tax’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CatalogAnalytics’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_Weee’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Dotdigitalgroup_Email’:  
Module ‘Magento_WishlistAnalytics’:  
Module ‘Shopial_Facebook’:  
Module ‘Temando_Shipping’:  
Data post-updates:  
Module ‘Magento_Store’:  
Module ‘Magento_Directory’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Config’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Theme’:  
Running data recurring…  
Module ‘Magento_Eav’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Customer’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Running data recurring…  
Module ‘Magento_Cms’:  
Module ‘Magento_Security’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Rule’:  
Module ‘Magento_Cron’:  
Module ‘Magento_Catalog’:  
Module ‘Magento_Search’:  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_Quote’:  
Module ‘Magento_SalesSequence’:  
Running data recurring…  
Module ‘Magento_Payment’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_User’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_CatalogInventory’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Integration’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_Bundle’:  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_InstantPurchase’:  
Module ‘Magento_Analytics’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Reports’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_QuoteAnalytics’:  
Module ‘Magento_ReleaseNotification’:  
Module ‘Magento_Review’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_ReviewAnalytics’:  
Module ‘Magento_Robots’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_SalesAnalytics’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_ConfigurableProductSales’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_CustomerAnalytics’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_Signifyd’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_Tax’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CatalogAnalytics’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_Weee’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Dotdigitalgroup_Email’:  
Module ‘Magento_WishlistAnalytics’:  
Module ‘Shopial_Facebook’:  
Module ‘Temando_Shipping’:  
Nothing to import.

{{< /highlight >}}

That’s it! Your Magento 2.2.3 is now ready on Valet+

You can access your frontend at: http://magento.test

Admin: http://magento.test/admin