## opendkim

#### Configuration

###### Initial setup
    `# apt-get install opendkim`
    `# mkdir /etc/opendkim/keys/mail.iostreamcomputing.net`
    `# opendkim-genkey -D /etc/opendkim/keys/mail.iostreamcomputing.net/ -d mail.iostreamcomputing.net -s default`
    `# chown -R opendkim: /etc/opendkim/keys/mail.iostreamcomputing.net`
    `# mv /etc/opendkim/keys/mail.iostreamcomputing.net/default.private /etc/opendkim/keys/mail.iostreamcomputing.net/default`

###### Set up key table
    Add to /etc/opendkim/KeyTable:
    `default._domainkey.mail.iostreamcomputing.net mail.iostreamcomputing.net:default:/etc/opendkim/keys/mail.iostreamcomputing.net/default

###### Set up signing table
    `*@iostreamcomputing.net default._domainkey.mail.iostreamcomputing.net`

###### Finishing up
    `# systemctl restart opendkim`
    `# systemctl reload postfix`

###### Useful article
    https://www.prosinger.net/opendkim-postfix/
