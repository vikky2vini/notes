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

###### Useful links:
  [Linode howto](https://www.linode.com/docs/email/postfix/email-with-postfix-dovecot-and-mysql)
  [Digital Ocean howto](https://www.digitalocean.com/community/tutorials/how-to-configure-a-mail-server-using-postfix-dovecot-mysql-and-spamassassin)
  [ClamSMTP article](http://thewalter.net/stef/software/clamsmtp/postfix.html)
