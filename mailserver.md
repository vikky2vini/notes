## Mail server notes

###### List all domains that the server is currently responsible for:
    SELECT * FROM mailserver.virtual_domains;

###### Add a new domain to the mail server:
    INSERT INTO `mailserver`.`virtual_domains` (`name`) VALUES ('mydomain.tld');

###### Create a new user:
    INSERT INTO `mailserver`.`virtual_users` (`id`, `domain_id`, `password` , `email`) VALUES ('2', '5', ENCRYPT('mypassword', CONCAT('$6$', SUBSTRING(SHA(RAND()), -16))), 'myuser@mydomain.tld');

###### Add a new mail alias (user must exist first):
    INSERT INTO `mailserver`.`virtual_aliases` (`domain_id`, `source`, `destination`) VALUES ('5', 'alias@mydomain.tld', 'mymail@mydomain.tld');

###### Required DNS entries for secondary domains:
    _dmarc  TXT  v=DMARC1; p=none
    @ MX 10 mail.mydomain.tld
    @ TXT v=spf1 a:mail.mydomain.tld a:jaylacroix.me ip4:<MAIL_SERVER_IP>

###### Setting up a new mail server (migrating configuration from existing)

  * Set up new droplet

  * apt-get update && apt-get dist-upgrade

  * reboot

  * `apt-get install mariadb-server`

  * `mysql_secure_installation` (set root password, etc)

  * Dump DB from old server:
    `mysqldump -u root -p --databases mailserver > mailserver.sql`

  * Import DB into new server:
    `mysql -u root -p < mailserver.sql`

  * In mariadb shell:
    `grant all privileges on mailserver.* to mailuser@localhost identified by '<password';`

  * Copy postfix configuration files to new server
    `scp -rp /etc/postfix root@<new_server>:/etc/`

  * Copy dovecot configuration files to new server:
    `scp -rp /etc/dovecot root@<new_server>:/etc/`

  * Copy SSL certificates to new server:
    `scp -rp /etc/certs root@<new_server>:/etc/`

  * Copy spamassassin configuration files to new server:
    `scp -rp /etc/spamassassin root@<new-server>:/etc/`
    `scp -rp /etc/default/spamassassin root@<new-server>:/etc/default`

  * Copy alias files to new server:
    `scp -rp /etc/aliases* root@<new-server>:/etc/`

  * Create /etc/mailname file:
    `echo 'mail.iostreamcomputing.net' > /etc/mailname`

  * Create vmail user:
    Add to /etc/passwd: `vmail:x:5000:5000::/var/mail:/bin/sh`
    Add to /etc/group: `vmail:x:5000:`
   Add to /etc/shadow: `vmail:!:16739:0:99999:7:::`

  * Install required packages:
    `apt-get install apache2 dovecot-core dovecot-imapd dovecot-lmtpd dovecot-managesieved dovecot-mysql dovecot-pop3d dovecot-sieve postfix postfix-mysql spamassassin`

  * Transfer email files from old server to new server:
   `scp -rp /var/mail/vhosts root@<new-server>:/var/mail/`
   `chown -R vmail: /var/mail`

  * Activate spamassassin
    `systemctl enable spamassassin`
    `systemctl start spamassassin`

  * Just in case: restart postfix, then dovecot

  * Create spamd user:
    Add to /etc/passwd: `spamd:x:5001:5001::/var/log/spamassassin:/bin/false`
    Add to /etc/group: `spamd:x:5001:`
    Add to /etc/shadow: `spamd:!:16743:0:99999:7:::`

  * Install roundcube packages:
    `apt-get install roundcube roundcube-mysql roundcube-plugins-extra`
    `dpkg-reconfigure roundcube-core`

  * Configure apache for roundcube:
    Add to /etc/apache2/sites-available/default-ssl.conf:
    `SSLCertificateFile /etc/certs/mail.iostreamcomputing.net.bundle`

    Add to /etc/apache2/sites-available/default-ssl.conf:
    `SSLCertificateKeyFile /etc/certs/mail.iostreamcomputing.net.key`

    Add to /etc/apache2/sites-available/default-ssl.conf:
    `SSLCACertificateFile /etc/certs/mail.iostreamcomputing.net.ca.bundle`

    Add to the end of /etc/apache2/sites-available/000-default.conf:
    `Redirect permanent / https://mail.iostreamcomputing.net/webmail`

    Edit /etc/roundcube/apache.conf:
    Change `Alias /roundcube /var/lib/roundcube` to `Alias /webmail /var/lib/roundcube`

  * Enable default ssl site in apache:
     `a2enmod ssl`
     `a2ensite default-ssl`

  * Edit /etc/config.inc.php and change `$config['default_host'] = ' '` to `$config['default_host'] = 'localhost'`

  * Edit `/etc/config.inc.php` and add `sieverules` to `$config['plugins'] = array()`

  * Edit: `/etc/roundcube/debian-db-roundcube.php` and add database password to `$dbpass='<pass here>';`

  * `cp /usr/share/roundcube/plugins/sieverules/config.inc.php.dist /etc/roundcube/plugins/sieverules/config.inc.php`

  * `systemctl restart apache2`

  * Clearing dovecot index (may or may not be necessary, but the index would've been copied from the old server while scp'ing the mail): rm /var/mail/vhosts/jaylacroix.me/jay/dovecot.index*


###### Useful links:
  [Linode howto](https://www.linode.com/docs/email/postfix/email-with-postfix-dovecot-and-mysql)
  [Digital Ocean howto](https://www.digitalocean.com/community/tutorials/how-to-configure-a-mail-server-using-postfix-dovecot-mysql-and-spamassassin)
  [ClamSMTP article](http://thewalter.net/stef/software/clamsmtp/postfix.html)
