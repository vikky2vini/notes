## Nextcloud

#### Previous issues:

######  memcache errors in config page:
  * install: `php5-apcu`
  * Edit: `/var/www/nextcloud/config/config.php`
     Add: `'memcache.local' => '\OC\Memcache\APCu'`

###### DAVDroid Syncing:
  * URL: `https://nextcloud.mydomain.tld/remote.php/dav/`
    (If nextcloud is a subdirectory, the URL would be:
    `https://server.tld/nextcloud/remote.php/dav/`
  * Mods to enable in Apache: headers env dir mime rewrite
  * Make sure the below configuration is added to the nextcloud virtual host:
		RewriteEngine on
        Redirect 301 /.well-known/carddav /remote.php/dav
        Redirect 301 /.well-known/caldav /remote.php/dav

        <Directory "/var/www/nextcloud.mydomain.tld">
                Options +FollowSymlinks
                Options Indexes MultiViews
                AllowOverride all
                Order allow,deny
                allow from all
                <IfModule mod_dav.c>
                    Dav off
                </IfModule>

                SetEnv HOME /var/www/nextcloud.mydomain.tld
                SetEnv HTTP_HOME /var/www/nextcloud.mydomain.tld
        </Directory>
