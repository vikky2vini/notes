## Quassel

###### Generate a new SSL certificate:
    openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /var/lib/quassel/quasselCert.pem -out /var/lib/quasselCert.pem
