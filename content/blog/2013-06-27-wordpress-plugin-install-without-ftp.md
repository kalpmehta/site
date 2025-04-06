---
id: 747
title: 'WordPress plugin install without FTP'
date: '2013-06-27T12:13:16+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=747'
permalink: /index.php/2013/06/27/wordpress-plugin-install-without-ftp/
crp_related_posts:
    - '<div class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2013/02/09/magento-500-internal-server-error/"     class="crp_title">Magento 500 internal server error</a></li><li><a href="http://ka.lpe.sh/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/"     class="crp_title">WordPress: Show total/aggregate ratings and reviews to your posts/pages</a></li><li><a href="http://ka.lpe.sh/2013/06/20/how-to-install-orocrm/"     class="crp_title">OroCRM Installation guide</a></li><li><a href="http://ka.lpe.sh/2013/02/20/magento-product-import-error-shows-html-code-while-importing/"     class="crp_title">Magento: Product Import error &#8211; shows HTML code while importing</a></li><li><a href="http://ka.lpe.sh/2012/10/22/humor-name-already-taken-lol/"     class="crp_title">Humor: Name already taken! LOL</a></li></ul></div>'
categories:
    - Wordpress
tags:
    - 'ftp connection information'
    - wordpress
---

![Wordpress Connection Information Error](http://ka.lpe.sh/wp-content/uploads/2013/06/wp_connection_error.jpg)

WordPress generally gives you page to fill FTP connection details when you try to install new plugin or update wordpress. The reason is it cannot write to wp-content directory due of lack of permissions to write. The best way is to change permissions and ownership of wp-content directory. But if you can’t do that because of some reason, then add the below line of code in your wp-config.php

{{< highlight php "style=emacs" >}}define(‘FS_METHOD’, ‘direct’);{{< /highlight >}}

Other way is to change permissions and ownerships to wp-content directory as said.  
{{< highlight http >}} chown -R www-data wordpress  
chgrp -R www-data wordpress  
chmod -R 755 wordpress/wp-content{{< /highlight >}}