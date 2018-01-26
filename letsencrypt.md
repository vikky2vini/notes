## Let's Encrypt

###### Install certbot
  `# add-apt-repository ppa:certbot/certbot`
  `# apt-get update`
  `# apt-get install python-certbot-apache`

###### Set up certificates
  `# certbot --apache -d example.com -d www.example.com`

###### Set up certificates (alternative method)
   As of 2018-01-26, the --apache method wasn't working.
   This may be a temporary issue.
   The following command did work:

  `# certbot --installer apache --authenticator webroot -d jaylacroix.com -d www.jaylacroix.com -w /var/www/jaylacroix.com`

###### Set up automatic certificate renewal
  The following cron line will automatically renew any certificates that are set to renew in less than 30 days.
  `0 1 * * * /usr/bin/certbot renew --quiet`
