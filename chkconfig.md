## chkconfig

###### To check whether or not a daemon is enabled at boot:
  `# /sbin/chkconfig --list mysqld`

###### If the service isn't listed in chkconfig, add it:
  `# /sbin/chkconfig --add mysqld`

###### To enable a service to start at boot:
  `# /sbin/chkconfig mysqld on`
