---
id: 747
title: 'WordPress plugin install without FTP'
date: '2013-06-27T12:13:16+00:00'
author: kalpesh
layout: post
tags:
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