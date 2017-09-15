## nagios

###### Source install procedure (tested on Ubuntu 16.04):
    `# apt-get install gcc make binutils cpp libpq-dev libmysqlclient-dev libssl1.0.0 libssl-dev pkg-config libgd2-xpm-dev libgd-tools perl libperl-dev libnet-snmp-perl snmp apache2 libapache2-mod-php unzip`

	`# mkdir /usr/src/nagios4`

	`# cd /usr/src/nagios4`

	`# tar –xzf /path/to/nagios-4.0.tar.gz`

	`# tar –xzf /path/to/nagios-plugins-1.4.16.tar.gz`

	`# groupadd nagios`

	`# groupadd nagioscmd`

	`# useradd -g nagios -G nagioscmd -d /opt/nagios nagios`

    `# usermod -aG nagioscmd www-data`

	`# mkdir -p /opt/nagios /etc/nagios /var/nagios`

	`# chown nagios:nagios /opt/nagios /etc/nagios /var/nagios`

	`# sh configure --prefix=/opt/nagios --sysconfdir=/etc/nagios --localstatedir=/var/nagios --libexecdir=/opt/nagios/plugins --with-command-group=nagioscmd`

	`# make all`

	`# cd ./base && make`

	`# make install`

	`# make install-commandmode`

	`# make install-config`

    `# cd plugindir`

	`# sh configure --prefix=/opt/nagios --sysconfdir=/etc/nagios --localstatedir=/var/nagios --libexecdir=/opt/nagios/plugins`

	`# make all`

	`# make install`

	copy startup file from git repository to /etc/init.d/nagios

	`# update-rc.d nagios defaults`

     Copy apache config file from git repository to /etc/apache2/conf-available/nagios

     `# a2enconf nagios`

     `# systemctl restart apache2`

     `# /etc/init.d/nagios restart`
