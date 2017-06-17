Show assigned DNS servers:
  nmcli dev show |grep DNS

Other commands that may show actual DNS servers:
  nmcli device show <interfacename> | grep IP4.DNS
  nmcli dev list iface <interfacename> | grep IP4
