---
id: 1096
title: 'Magento 2 upgrade from 2.0.* to latest version using composer via CLI'
date: '2017-04-17T01:11:15+00:00'
author: kalpesh
layout: post
tags:
    - Magento2
tags:
    - composer
    - 'magento 2 upgrade'
    - 'magento 2.0 to 2.1'
---

In this post I will show you how to upgrade Magento 2.0.5 (2.0.*) to 2.1.6 which is latest CE version as of today. We will do it using composer via server command-line interface. It is recommended to take code and DB backup and do this upgrade on your development/stage server first.

Magento 2 comes with Web Setup Wizard (under Admin > System) where you can upgrade from admin panel itself, but for some reason it was always failing for me at Readiness Check’s Component Dependency check.

Step 1.) Edit the composer.json which should be located at the root of your store. Change **version** and **magento/product-community-edition** from 2.0.* (whatever you have currently) to 2.1.6 or any latest version you wish to upgrade to. Also change sample data versions from 100.0.* to 100.1.*  
{{< highlight http >}} {  
 “name”: “magento/project-community-edition”,  
 “description”: “eCommerce Platform for Growth (Community Edition)”,  
 “type”: “project”,  
 “version”: “2.1.6”,  
 “require”: {  
 “magento/product-community-edition”: “2.1.6”,  
 “composer/composer”: “@alpha”,  
 “magento/module-bundle-sample-data”: “100.1.*”,  
 “magento/module-theme-sample-data”: “100.1.*”,  
 “magento/module-widget-sample-data”: “100.1.*”,  
 “magento/module-catalog-sample-data”: “100.1.*”,  
 “magento/module-customer-sample-data”: “100.1.*”,  
 “magento/module-cms-sample-data”: “100.1.*”,  
 “magento/module-tax-sample-data”: “100.1.*”,  
 “magento/module-review-sample-data”: “100.1.*”,  
 “magento/module-catalog-rule-sample-data”: “100.1.*”,  
 “magento/module-sales-rule-sample-data”: “100.1.*”,  
 “magento/module-sales-sample-data”: “100.1.*”,  
 “magento/module-grouped-product-sample-data”: “100.1.*”,  
 “magento/module-downloadable-sample-data”: “100.1.*”,  
 “magento/module-msrp-sample-data”: “100.1.*”,  
 “magento/module-configurable-sample-data”: “100.1.*”,  
 “magento/module-product-links-sample-data”: “100.1.*”,  
 “magento/module-wishlist-sample-data”: “100.1.*”,  
 “magento/module-swatches-sample-data”: “100.1.*”,  
 “magento/sample-data-media”: “100.1.*”,  
 “magento/module-offline-shipping-sample-data”: “100.1.*”  
 },…{{< /highlight >}}

Step 2.) composer update (Run this command on the server/terminal. You may need to create GitHub OAuth token to pass the rate limit. Login to your Github account (or create one) and head to Developer Settings > Personal access tokens and generate new token with full control of private repositories.)  
  
{{< highlight http >}} [user@server magento2]# composer update  
Loading composer repositories with package information  
Updating dependencies (including require-dev)  
Package operations: 12 installs, 183 updates, 0 removals  
 – Updating magento/magento-composer-installer (0.1.7 => 0.1.12): Downloading (connecting…)  
Could not fetch https://api.github.com/repos/magento/magento-composer-installer/zipball/10c600e88ad34ffc71bb7b435ea8415ce92d51de, please create a GitHub OAuth token to go over the API rate limit  
Head to https://github.com/settings/tokens/new?scopes=repo&amp;description=Composer+on+domain.com+1942  
to retrieve a token. It will be stored in “/root/.composer/auth.json” for future use by Composer.  
Token (hidden):  
Token stored successfully.  
Downloading (100%)  
 – Updating zendframework/zend-stdlib (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-validator (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-escaper (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-uri (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-loader (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-http (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating symfony/process (v2.8.4 => v2.8.19): Downloading (100%)  
 – Updating magento/framework (100.0.7 => 100.1.6): Downloading (100%)  
 – Updating magento/language-zh_hans_cn (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-pt_br (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-nl_nl (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-fr_fr (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-es_es (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-en_us (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/language-de_de (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/theme-frontend-blank (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/theme-frontend-luma (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/theme-adminhtml-backend (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-media-storage (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-config (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-backend (100.0.6 => 100.1.3): Downloading (100%)  
 – Updating magento/module-require-js (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-translation (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-theme (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-directory (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-store (100.0.6 => 100.1.5): Downloading (100%)  
 – Updating magento/module-ui (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-user (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-email (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-variable (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-authorization (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-quote (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-catalog-inventory (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-eav (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-catalog (100.0.6 => 101.0.6): Downloading (100%)  
 – Updating magento/module-page-cache (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-url-rewrite (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-cms-url-rewrite (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-cms (100.0.5 => 101.0.4): Downloading (100%)  
 – Updating magento/module-catalog-url-rewrite (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-import-export (100.0.5 => 100.1.4): Downloading (100%)  
 – Installing magento/module-security (100.1.3): Downloading (100%)  
 – Updating magento/module-customer (100.0.6 => 100.1.5): Downloading (100%)  
 – Updating magento/module-integration (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-widget (100.0.6 => 100.1.2): Downloading (100%)  
 – Updating magento/module-tax (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-reports (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-sales-rule (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-rule (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-catalog-rule (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-sales (100.0.6 => 100.1.5): Downloading (100%)  
 – Updating magento/module-shipping (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-payment (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-checkout (100.0.6 => 100.1.5): Downloading (100%)  
 – Updating magento/module-msrp (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-grouped-product (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-wishlist (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-rss (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-gift-message (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-sales-sequence (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-contact (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-downloadable (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-cron (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-newsletter (100.0.6 => 100.1.2): Downloading (100%)  
 – Updating magento/module-review (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-product-alert (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-indexer (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-catalog-import-export (100.0.6 => 100.1.4): Downloading (100%)  
 – Updating magento/module-developer (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-backup (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-weee (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-webapi (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-webapi-security (100.0.1 => 100.1.2): Downloading (100%)  
 – Updating magento/module-version (100.0.5 => 100.1.2): Downloading (100%)  
 – Installing magento/module-vault (100.2.1): Downloading (100%)  
 – Updating magento/module-usps (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-ups (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-tax-import-export (100.0.5 => 100.1.2): Downloading (100%)  
 – Installing magento/module-swatches-layered-navigation (100.1.2): Downloading (100%)  
 – Updating magento/module-configurable-product (100.0.5 => 100.1.6): Downloading (100%)  
 – Updating magento/module-swatches (100.0.6 => 100.1.5): Downloading (100%)  
 – Updating magento/module-swagger (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-sitemap (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-send-friend (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-search (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-catalog-search (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-sample-data (100.0.5 => 100.1.3): Downloading (100%)  
 – Installing magento/module-sales-inventory (100.1.1): Downloading (100%)  
 – Updating magento/module-product-video (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-persistent (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-paypal (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-offline-shipping (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-offline-payments (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-new-relic-reporting (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-multishipping (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-layered-navigation (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-grouped-import-export (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-cookie (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-google-analytics (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-google-optimizer (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-google-adwords (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-fedex (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-encryption-key (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-downloadable-import-export (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-dhl (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-deploy (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-customer-import-export (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-currency-symbol (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-configurable-import-export (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-checkout-agreements (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-catalog-widget (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-catalog-rule-configurable (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-captcha (100.0.6 => 100.1.3): Downloading (100%)  
 – Updating magento/module-cache-invalidate (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating magento/module-bundle (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-bundle-import-export (100.0.5 => 100.1.3): Downloading (100%)  
 – Updating braintree/braintree_php (2.39.0 => 3.7.0): Downloading (100%)  
 – Updating magento/module-braintree (100.0.5 => 100.1.5): Downloading (100%)  
 – Updating magento/module-authorizenet (100.0.5 => 100.1.4): Downloading (100%)  
 – Updating magento/module-advanced-pricing-import-export (100.0.6 => 100.1.2): Downloading (100%)  
 – Updating magento/module-admin-notification (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating magento/module-marketplace (100.0.5 => 100.1.2): Downloading (100%)  
 – Updating psr/log (1.0.0 => 1.0.2): Downloading (100%)  
 – Updating symfony/finder (v2.8.4 => v3.2.7): Downloading (100%)  
 – Updating symfony/filesystem (v2.8.4 => v2.8.19): Downloading (100%)  
 – Installing seld/phar-utils (1.0.1): Downloading (100%)  
 – Updating seld/jsonlint (1.4.0 => 1.6.0): Downloading (100%)  
 – Installing seld/cli-prompt (1.0.3): Downloading (100%)  
 – Installing composer/spdx-licenses (1.1.6): Downloading (100%)  
 – Installing composer/semver (1.4.2): Downloading (100%)  
 – Updating composer/composer (1.0.0-alpha10 => 1.0.0-beta1): Downloading (100%)  
 – Updating magento/composer (1.0.2 => 1.0.3): Downloading (100%)  
 – Updating phpseclib/phpseclib (0.3.10 => 2.0.4): Downloading (100%)  
 – Updating symfony/event-dispatcher (v2.8.4 => v2.8.19): Downloading (100%)  
 – Updating oyejorge/less.php (v1.7.0.3 => v1.7.0.14): Downloading (100%)  
 – Installing colinmollenhour/cache-backend-file (1.4): Downloading (100%)  
 – Installing colinmollenhour/cache-backend-redis (1.9): Downloading (100%)  
 – Installing colinmollenhour/credis (1.6): Downloading (100%)  
 – Updating magento/zendframework1 (1.12.16 => 1.12.16-patch3): Downloading (100%)  
 – Installing colinmollenhour/php-redis-session-abstract (v1.2): Downloading (100%)  
 – Updating zendframework/zend-servicemanager (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-log (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-math (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-json (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-serializer (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-eventmanager (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-code (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-di (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-filter (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-inputfilter (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-form (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-config (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-view (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-i18n (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-text (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-mvc (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-modulemanager (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-console (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-crypt (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-server (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating zendframework/zend-soap (2.4.9 => 2.4.11): Downloading (100%)  
 – Updating magento/magento2-base (2.0.5 => 2.1.6): Downloading (100%)  
 – Updating magento/module-catalog-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-bundle-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-widget-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-customer-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/sample-data-media (100.0.4 => 100.1.0): Downloading (100%)  
 – Updating magento/module-theme-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-cms-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-tax-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-review-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-catalog-rule-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-sales-rule-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-product-links-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-configurable-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-sales-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-grouped-product-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-downloadable-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-msrp-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-wishlist-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-swatches-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating magento/module-offline-shipping-sample-data (100.0.5 => 100.1.1): Downloading (100%)  
 – Updating phpunit/php-timer (1.0.7 => 1.0.9): Downloading (100%)  
 – Updating sebastian/recursion-context (1.0.2 => 1.0.5): Downloading (100%)  
 – Updating sebastian/exporter (1.2.1 => 1.2.2): Downloading (100%)  
 – Updating sebastian/comparator (1.2.0 => 1.2.4): Downloading (100%)  
 – Updating sebastian/environment (1.3.5 => 1.3.8): Downloading (100%)  
 – Updating symfony/yaml (v2.8.4 => v2.8.19): Downloading (100%)  
 – Updating symfony/config (v2.8.4 => v2.8.19): Downloading (100%)  
 – Updating symfony/dependency-injection (v2.8.4 => v2.8.19): Downloading (100%)  
 – Updating symfony/stopwatch (v3.0.4 => v3.2.7): Downloading (100%)  
 – Updating fabpot/php-cs-fixer (v1.11.2 => v1.13.1): Downloading (100%)  
 – Updating phpunit/php-token-stream (1.4.8 => 1.4.11): Downloading (100%)  
Package fabpot/php-cs-fixer is abandoned, you should avoid using it. Use friendsofphp/php-cs-fixer instead.  
Writing lock file  
Generating autoload files  
Deprecation Notice: The callback MagentoHackathon\\Composer\\Magento\\Plugin::onNewCodeEvent declared at /var/www/magento2/vendor/magento/magento-composer-installer/src/MagentoHackathon/Composer/Magento/Plugin.php accepts a Composer\\Script\\CommandEvent but post-update-cmd events use a Composer\\Script\\Event instance. Please adjust your type hint accordingly, see https://getcomposer.org/doc/articles/scripts.md#event-classes in phar:///usr/local/bin/composer/src/Composer/EventDispatcher/EventDispatcher.php:314  
You have new mail in /var/spool/mail/root{{< /highlight >}}

Step 3.) rm -rf var/cache/* var/di/* var/generation/* var/page_cache/*

Step 4.) php bin/magento cache:flush

Step 5.) php bin/magento setup:upgrade

{{< highlight http >}} Cache cleared successfully  
File system cleanup:  
/var/www/marketiny/magento2/var/generation/Composer  
/var/www/marketiny/magento2/var/generation/Magento  
/var/www/marketiny/magento2/var/generation/Symfony  
The directory ‘/var/www/marketiny/magento2/var/di/’ doesn’t exist – skipping cleanup  
/var/www/marketiny/magento2/pub/static/_requirejs  
/var/www/marketiny/magento2/pub/static/adminhtml  
/var/www/marketiny/magento2/pub/static/deployed_version.txt  
/var/www/marketiny/magento2/pub/static/frontend  
/var/www/marketiny/magento2/var/view_preprocessed/css  
/var/www/marketiny/magento2/var/view_preprocessed/html  
/var/www/marketiny/magento2/var/view_preprocessed/source  
Updating modules:  
Schema creation/updates:  
Module ‘Deven_Automation’:  
Module ‘Magento_Store’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Directory’:  
Module ‘Magento_Theme’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Customer’:  
Upgrading schema..  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Module ‘Magento_Cms’:  
Upgrading schema..  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Catalog’:  
Upgrading schema..  
Module ‘Magento_Rule’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_Search’:  
Upgrading schema..  
Module ‘Magento_Bundle’:  
Upgrading schema..  
Module ‘Magento_Quote’:  
Upgrading schema..  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_Payment’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_Config’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Cron’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_User’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_CustomerSampleData’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_CatalogInventory’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_CatalogRule’:  
Upgrading schema..  
Module ‘Magento_Sales’:  
Upgrading schema..  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_Tax’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_Vault’:  
Installing schema…  
Module ‘Magento_Security’:  
Installing schema… Upgrading schema…  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_MsrpSampleData’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Upgrading schema..  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Weee’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_CatalogSampleData’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_Reports’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Review’:  
Module ‘Magento_DownloadableSampleData’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShippingSampleData’:  
Module ‘Magento_BundleSampleData’:  
Module ‘Magento_ConfigurableSampleData’:  
Module ‘Magento_ThemeSampleData’:  
Module ‘Magento_ProductLinksSampleData’:  
Module ‘Magento_ReviewSampleData’:  
Module ‘Magento_Integration’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_CatalogRuleSampleData’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_SwatchesSampleData’:  
Module ‘Magento_GroupedProductSampleData’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_TaxSampleData’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_CmsSampleData’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_SalesRuleSampleData’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_SalesSampleData’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Magento_WidgetSampleData’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_WishlistSampleData’:  
Schema post-updates:  
Module ‘Deven_Automation’:  
Module ‘Magento_Store’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Directory’:  
Module ‘Magento_Theme’:  
Module ‘Magento_Backend’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Customer’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Running schema recurring…  
Module ‘Magento_Cms’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Catalog’:  
Running schema recurring…  
Module ‘Magento_Rule’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_Search’:  
Module ‘Magento_Bundle’:  
Running schema recurring…  
Module ‘Magento_Quote’:  
Module ‘Magento_CatalogUrlRewrite’:  
Running schema recurring…  
Module ‘Magento_Widget’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_Payment’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_Config’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Cron’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_User’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_CustomerSampleData’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_CatalogInventory’:  
Running schema recurring…  
Module ‘Magento_ImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_Tax’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Security’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Running schema recurring…  
Module ‘Magento_MsrpSampleData’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Weee’:  
Running schema recurring…  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Running schema recurring…  
Module ‘Magento_CatalogSampleData’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_Reports’:  
Running schema recurring…  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Review’:  
Module ‘Magento_DownloadableSampleData’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShippingSampleData’:  
Module ‘Magento_BundleSampleData’:  
Module ‘Magento_ConfigurableSampleData’:  
Module ‘Magento_ThemeSampleData’:  
Module ‘Magento_ProductLinksSampleData’:  
Module ‘Magento_ReviewSampleData’:  
Module ‘Magento_Integration’:  
Running schema recurring…  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_CatalogRuleSampleData’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_SwatchesSampleData’:  
Module ‘Magento_GroupedProductSampleData’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_TaxSampleData’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_CmsSampleData’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_SalesRuleSampleData’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_SalesSampleData’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Magento_WidgetSampleData’:  
Module ‘Magento_Wishlist’:  
Running schema recurring…  
Module ‘Magento_WishlistSampleData’:  
DDL cache cleared successfully  
Data install/update:  
Module ‘Deven_Automation’:  
Module ‘Magento_Store’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Directory’:  
Module ‘Magento_Theme’:  
Upgrading data..  
Module ‘Magento_Backend’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Customer’:  
Upgrading data..  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Module ‘Magento_Cms’:  
Upgrading data..  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Catalog’:  
Upgrading data..  
Module ‘Magento_Rule’:  
Module ‘Magento_Msrp’:  
Upgrading data..  
Module ‘Magento_Search’:  
Module ‘Magento_Bundle’:  
Upgrading data..  
Module ‘Magento_Quote’:  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_Payment’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_Config’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Cron’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_User’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_CustomerSampleData’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_CatalogInventory’:  
Upgrading data..  
Module ‘Magento_ImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_Sales’:  
Upgrading data..  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Upgrading data..  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Upgrading data..  
Module ‘Magento_Tax’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_Vault’:  
Upgrading data…  
Module ‘Magento_Security’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_MsrpSampleData’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Weee’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_CatalogSampleData’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_Reports’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Review’:  
Module ‘Magento_DownloadableSampleData’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShippingSampleData’:  
Module ‘Magento_BundleSampleData’:  
Module ‘Magento_ConfigurableSampleData’:  
Module ‘Magento_ThemeSampleData’:  
Module ‘Magento_ProductLinksSampleData’:  
Module ‘Magento_ReviewSampleData’:  
Module ‘Magento_Integration’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_CatalogRuleSampleData’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Upgrading data..  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_SwatchesSampleData’:  
Module ‘Magento_GroupedProductSampleData’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_TaxSampleData’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_CmsSampleData’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_SalesRuleSampleData’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_SalesSampleData’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Magento_WidgetSampleData’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_WishlistSampleData’:  
Data post-updates:  
Module ‘Deven_Automation’:  
Module ‘Magento_Store’:  
Module ‘Magento_AdvancedPricingImportExport’:  
Module ‘Magento_Directory’:  
Module ‘Magento_Theme’:  
Running data recurring…  
Module ‘Magento_Backend’:  
Module ‘Magento_Backup’:  
Module ‘Magento_Eav’:  
Module ‘Magento_Customer’:  
Module ‘Magento_BundleImportExport’:  
Module ‘Magento_AdminNotification’:  
Module ‘Magento_CacheInvalidate’:  
Module ‘Magento_Indexer’:  
Module ‘Magento_Cms’:  
Module ‘Magento_CatalogImportExport’:  
Module ‘Magento_Catalog’:  
Module ‘Magento_Rule’:  
Module ‘Magento_Msrp’:  
Module ‘Magento_Search’:  
Module ‘Magento_Bundle’:  
Module ‘Magento_Quote’:  
Module ‘Magento_CatalogUrlRewrite’:  
Module ‘Magento_Widget’:  
Module ‘Magento_SalesSequence’:  
Module ‘Magento_CheckoutAgreements’:  
Module ‘Magento_Payment’:  
Module ‘Magento_SampleData’:  
Module ‘Magento_CmsUrlRewrite’:  
Module ‘Magento_Config’:  
Module ‘Magento_ConfigurableImportExport’:  
Module ‘Magento_Downloadable’:  
Module ‘Magento_CatalogSearch’:  
Module ‘Magento_Contact’:  
Module ‘Magento_Cookie’:  
Module ‘Magento_Cron’:  
Module ‘Magento_CurrencySymbol’:  
Module ‘Magento_User’:  
Module ‘Magento_CustomerImportExport’:  
Module ‘Magento_CustomerSampleData’:  
Module ‘Magento_Deploy’:  
Module ‘Magento_Developer’:  
Module ‘Magento_Dhl’:  
Module ‘Magento_Authorization’:  
Module ‘Magento_CatalogInventory’:  
Module ‘Magento_ImportExport’:  
Module ‘Magento_CatalogRule’:  
Module ‘Magento_Sales’:  
Module ‘Magento_Email’:  
Module ‘Magento_EncryptionKey’:  
Module ‘Magento_Fedex’:  
Module ‘Magento_GiftMessage’:  
Module ‘Magento_Checkout’:  
Module ‘Magento_GoogleAnalytics’:  
Module ‘Magento_Ui’:  
Module ‘Magento_GroupedImportExport’:  
Module ‘Magento_GroupedProduct’:  
Module ‘Magento_Tax’:  
Module ‘Magento_DownloadableImportExport’:  
Module ‘Magento_Vault’:  
Module ‘Magento_Security’:  
Module ‘Magento_LayeredNavigation’:  
Module ‘Magento_Marketplace’:  
Module ‘Magento_MediaStorage’:  
Module ‘Magento_ConfigurableProduct’:  
Module ‘Magento_MsrpSampleData’:  
Module ‘Magento_Multishipping’:  
Module ‘Magento_NewRelicReporting’:  
Module ‘Magento_Newsletter’:  
Module ‘Magento_OfflinePayments’:  
Module ‘Magento_SalesRule’:  
Module ‘Magento_OfflineShipping’:  
Module ‘Magento_PageCache’:  
Module ‘Magento_Weee’:  
Module ‘Magento_Paypal’:  
Module ‘Magento_Persistent’:  
Module ‘Magento_ProductAlert’:  
Module ‘Magento_CatalogSampleData’:  
Module ‘Magento_ProductVideo’:  
Module ‘Magento_Captcha’:  
Module ‘Magento_Reports’:  
Module ‘Magento_RequireJs’:  
Module ‘Magento_Review’:  
Module ‘Magento_DownloadableSampleData’:  
Module ‘Magento_Rss’:  
Module ‘Magento_CatalogRuleConfigurable’:  
Module ‘Magento_Authorizenet’:  
Module ‘Magento_SalesInventory’:  
Module ‘Magento_OfflineShippingSampleData’:  
Module ‘Magento_BundleSampleData’:  
Module ‘Magento_ConfigurableSampleData’:  
Module ‘Magento_ThemeSampleData’:  
Module ‘Magento_ProductLinksSampleData’:  
Module ‘Magento_ReviewSampleData’:  
Module ‘Magento_Integration’:  
Module ‘Magento_SendFriend’:  
Module ‘Magento_Shipping’:  
Module ‘Magento_Sitemap’:  
Module ‘Magento_CatalogRuleSampleData’:  
Module ‘Magento_Swagger’:  
Module ‘Magento_Swatches’:  
Module ‘Magento_SwatchesLayeredNavigation’:  
Module ‘Magento_SwatchesSampleData’:  
Module ‘Magento_GroupedProductSampleData’:  
Module ‘Magento_TaxImportExport’:  
Module ‘Magento_TaxSampleData’:  
Module ‘Magento_GoogleAdwords’:  
Module ‘Magento_CmsSampleData’:  
Module ‘Magento_Translation’:  
Module ‘Magento_GoogleOptimizer’:  
Module ‘Magento_Ups’:  
Module ‘Magento_UrlRewrite’:  
Module ‘Magento_SalesRuleSampleData’:  
Module ‘Magento_Usps’:  
Module ‘Magento_Variable’:  
Module ‘Magento_Braintree’:  
Module ‘Magento_Version’:  
Module ‘Magento_Webapi’:  
Module ‘Magento_WebapiSecurity’:  
Module ‘Magento_SalesSampleData’:  
Module ‘Magento_CatalogWidget’:  
Module ‘Magento_WidgetSampleData’:  
Module ‘Magento_Wishlist’:  
Module ‘Magento_WishlistSampleData’:  
Please re-run Magento compile command{{< /highlight >}}

Step 6.) php bin/magento setup:di:compile

{{< highlight http >}} Compilation was started.  
Interception cache generation… 7/7 [============================] 100% 3 mins 408.2 MiBB0 MiB  
Generated code and dependency injection configuration successfully.{{< /highlight >}}

Step 7.) php bin/magento –version

{{< highlight http >}} Magento CLI version 2.1.6{{< /highlight >}}