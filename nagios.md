## nagios

###### Source install procedure (tested on Ubuntu 16.04):
    Note: Provision Ansible on the host LAST (Ansible creates a nagios user when it does the nrpe config)

    `# apt install gcc make binutils cpp libpq-dev libmysqlclient-dev libssl1.0.0 libssl-dev pkg-config libgd2-xpm-dev libgd-tools perl libperl-dev libnet-snmp-perl snmp apache2 libapache2-mod-php unzip`

    `# a2enmod authz_groupfile cgi`

	`# mkdir /usr/src/nagios4`

	`# cd /usr/src/nagios4`

	`# tar –xvf /path/to/nagios-4.0.tar.gz`

	`# tar –xvf /path/to/nagios-plugins-1.4.16.tar.gz`

	`# groupadd nagios`

	`# groupadd nagioscmd`

	`# useradd -g nagios -G nagioscmd -d /opt/nagios nagios`

    `# usermod -aG nagioscmd www-data`

	`# mkdir -p /opt/nagios /etc/nagios /var/nagios`

	`# chown nagios:nagios /opt/nagios /etc/nagios /var/nagios`

	`# sh configure --prefix=/opt/nagios --sysconfdir=/etc/nagios --localstatedir=/var/nagios --libexecdir=/opt/nagios/plugins --with-command-group=nagioscmd`

    `# chown nagios:nagioscmd -R /var/nagios/rw`

	`# make all`

	`# cd ./base && make`

	`# make install`

	`# make install-commandmode`

	`# make install-config`

    `# cd plugindir`

	`# sh configure --prefix=/opt/nagios --sysconfdir=/etc/nagios --localstatedir=/var/nagios --libexecdir=/opt/nagios/plugins`

	`# make all`

	`# make install`

    Clone the git repo

	copy startup file from git repository to /etc/init.d/nagios

	`# update-rc.d nagios defaults`

    `# mkdir -p /var/nagios/spool/checkresults`

    `# chown nagios: /var/nagios/spool/checkresults`

    Copy apache config file from git repository to /etc/apache2/conf-available/nagios.conf

    `# a2enconf nagios`

    `# systemctl restart apache2`

    `# /etc/init.d/nagios restart`

    Final steps:
      Copy check_nrpe to /opt/nagios/plugins/check_nrpe
      Add these lines to sudoers:
        nagios ALL=(ALL) NOPASSWD: /usr/lib/nagios/plugins/check_dhcp
        nagios ALL=(ALL) NOPASSWD: /bin/journalctl
        nagios ALL=(ALL) NOPASSWD: /etc/init.d/apache2
        nagios ALL=(ALL) NOPASSWD: /etc/init.d/nagios
        nagios ALL=(ALL) NOPASSWD: /etc/init.d/nagios
      For Telegram alerter:
        sudo pip install twx.botapi
