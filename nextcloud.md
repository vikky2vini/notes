## Nextcloud

#### Previous issues:

######  memcache errors in config page
  * install: `php5-apcu`
  * Edit: `/var/www/nextcloud/config/config.php`
     Add: `'memcache.local' => '\OC\Memcache\APCu'`

###### Collabora Office
  * `a2enmod proxy`
  * `a2enmod proxy_wstunnel`
  * `a2enmod proxy_http`
  * `apt-get install docker.io`
  * `docker run -t -d -p 127.0.0.1:9980:9980 -e 'domain=nextcloud\\.mydomain\\.net' --restart always --cap-add MKNOD collabora/code`
  * Add virtual host file (below)
  * `sudo certbot --installer apache --authenticator webroot -d office.mydomain.net`

Virtual host file for collabora:
<VirtualHost *:443>
ServerName office.mydomain.net:443

# Encoded slashes need to be allowed
AllowEncodedSlashes NoDecode

# keep the host
ProxyPreserveHost On

# static html, js, images, etc. served from loolwsd
# loleaflet is the client part of LibreOffice Online
ProxyPass           /loleaflet https://127.0.0.1:9980/loleaflet retry=0
ProxyPassReverse    /loleaflet https://127.0.0.1:9980/loleaflet

# WOPI discovery URL
ProxyPass           /hosting/discovery https://127.0.0.1:9980/hosting/discovery retry=0
ProxyPassReverse    /hosting/discovery https://127.0.0.1:9980/hosting/discovery

# Main websocket
ProxyPassMatch "/lool/(.*)/ws$" wss://127.0.0.1:9980/lool/$1/ws nocanon

# Admin Console websocket
ProxyPass   /lool/adminws wss://127.0.0.1:9980/lool/adminws

# Download as, Fullscreen presentation and Image upload operations
ProxyPass           /lool https://127.0.0.1:9980/lool
ProxyPassReverse    /lool https://127.0.0.1:9980/lool

# Container uses a unique non-signed certificate
SSLProxyEngine On
SSLProxyVerify None
SSLProxyCheckPeerCN Off
SSLProxyCheckPeerName Off

</VirtualHost>

###### DAVDroid Syncing
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

###### Previous Issues

#### e-book reader not saving bookmarks
    * Add the following lines to /var/www/nextcloud.domain.net/config/config.php:
        'overwrite.cli.url' => 'https://nextcloud.domain.net',
        'htaccess.RewriteBase' => '/',
    * Run the following command:
        `sudo -u www-data php /var/www/nextcloud.domain.net/occ maintenance:update:htaccess`

