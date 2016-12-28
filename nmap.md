## nmap

###### Scan a single host or an IPv4 address:
  `# nmap 172.16.254.10`
  `$ nmap server1.mydomain.com`

###### Scan a host name or IP with more info:
  `$ nmap -v 172.16.254.0`

###### Scan multiple IP addresses:
  `$ nmap 172.16.254.10 172.16.254.13`

###### Scan a range of IP addresses:
  `$ nmap 172.16.254.10-50`

###### Scan a range of IP addresses using a wildcard:
  `$ nmap 172.16.254.*`

###### Scan an entire subnet:
  `$ nmap 172.16.254.0/24`

###### Excluding hosts from a scan:
  `$ nmap 172.16.254.0/24 --exclude 172.16.254.10`
  `$ nmap 172.16.254.0/24 --exclude 172.16.254.10,172.16.254.11`

###### Turn on OS and version detection scanning:
  `$ nmap -A 172.16.254.10`
  `$ nmap -v -A 172.16.254.10`

###### Determine if a host or network is protected by a firewall:
  `$ nmap -sA 172.16.254.10`

###### Scan a host when its protected by a firewall:
  `$ nmap -PN 172.16.254.10`

###### Scan a network and find out which servers and devices are up and running:
  `$ nmap -sP 172.16.254.0/24`

###### Perform a fast scan:
  `$ nmap -F 172.16.254.10`

###### Display the reason a port is in a particular state:
  `$ nmap --reason 192.168.1.1`

###### Show all packets sent and received:
  `$ nmap --packet-trace 172.16.254.10`

###### Show host interfaces and routes:
  `$ nmap --iflist`

###### Scan specific ports:
  `$ nmap -p 80 172.16.254.10`
  `$ nmap -p T:80 172.16.254.10`
  `$ nmap -p U:80 172.16.254.10`
  `$ nmap -p 80,443 172.16.254.10` (two ports)
  `$ nmap -p 80-200 172.16.254.10` (range)

###### The fastest way to scan all your devices/computers for open ports ever:
  `$ nmap -T5 172.16.254.0/24`

###### Detect remote operating system:
  `$ nmap -O 172.16.254.10`

###### Scan and detect remote services with version information:
  `$ nmap -sV 172.16.254.10`

###### Scan a firewall for security weaknesses:
  `$ nmap -sN 192.168.1.254` (Fool the firewall into generating a response)
  `$ nmap -sF 192.168.1.254` (TCP FIN scan)
  `$ nmap -sX 192.168.1.254` (TCP Xmas scan, lighting the packets up like a Christmas tree)

###### Cloak a scan with decoys:
  `$ nmap -n -Ddecoy-ip1,decoy-ip2,your-own-ip,decoy-ip3,decoy-ip4 remote-host-ip`
  `$ nmap -n -D192.168.1.5,10.5.1.2,172.1.2.4,3.4.2.1 192.168.1.5`

###### Scan a firewall for MAC address spoofing:
  `$ nmap --spoof-mac MAC-ADDRESS-HERE 192.168.1.1` (Spoof your Mac address)
  `$ nmap -v -sT -PN --spoof-mac 0 192.168.1.1` (Make nmap choose a random MAC address)