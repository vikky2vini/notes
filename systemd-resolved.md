Show assigned DNS servers:
  systemd-resolve --status |grep DNS\ Servers

Disable listening on port 53 (this caused an issue with dnsmasq on pi-hole):
  Edit /etc/systemd/resolved.conf and add:
  DNSStubListener=no
