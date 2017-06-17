## Subsonic

Change which IP address subsonic listens on:
  edit /usr/share/subsonic/subsonic.sh
  change --host=?* to --host=172.16.249.10

Other commands that may show actual DNS servers:
  nmcli device show <interfacename> | grep IP4.DNS
  nmcli dev list iface <interfacename> | grep IP4
