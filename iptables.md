## iptables

###### Delete existing rules:
  `# iptables -F`

###### Delete existing rules (alternate method):
  `# iptables --flush`

###### Det default chain policies (default is ACCEPT):
  `# iptables -P INPUT DROP`
  `# iptables -P FORWARD DROP`
  `# iptables -P OUTPUT DROP`

###### Block a specific IP address:
  `# BLOCK_THIS_IP="x.x.x.x"`
  `# iptables -A INPUT -s "$BLOCK_THIS_IP" -j DROP`

###### Block TCP traffic on eth0 for a specific IP address:
  `# iptables -A INPUT -i eth0 "$BLOCK_THIS_IP" -j DROP`
  `# iptables -A INPUT -i eth0 -p tcp -s "$BLOCK_THIS_IP" -j DROP`

###### Allow ALL incoming SSH connections:
  `# iptables -A INPUT -i eth0 -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`

###### Allow incoming SSH only from a specific network:
  `# iptables -A INPUT -i eth0 -p tcp -s 192.168.100.0/24 --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT`

###### Allow outgoing SSH:
  `# iptables -A OUTPUT -o eth0 -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A INPUT -i eth0 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT`

###### Allow outgoing SSH only to a specific network:
  `# iptables -A OUTPUT -o eth0 -p tcp -d 192.168.100.0/24 --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A INPUT -i eth0 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT`

###### Allow incoming HTTP:
  `# iptables -A INPUT -i eth0 -p tcp --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT`

###### Allow incoming HTTPS:
  `# iptables -A INPUT -i eth0 -p tcp --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT`

###### Allow outgoing HTTPS:
  `# iptables -A OUTPUT -o eth0 -p tcp --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A INPUT -i eth0 -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT`

###### Combine multiple rules together using MultiPorts:
  `# iptables -A INPUT -i eth0 -p tcp -m multiport --dports 22,80,443 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp -m multiport --sports 22,80,443 -m state --state ESTABLISHED -j ACCEPT`

###### Load balance incoming web traffic:
  `# iptables -A PREROUTING -i eth0 -p tcp --dport 443 -m state --state NEW -m nth --counter 0 --every 3 --packet 0 -j DNAT --to-destination 192.168.1.101:443`
  `# iptables -A PREROUTING -i eth0 -p tcp --dport 443 -m state --state NEW -m nth --counter 0 --every 3 --packet 1 -j DNAT --to-destination 192.168.1.102:443`
  `# iptables -A PREROUTING -i eth0 -p tcp --dport 443 -m state --state NEW -m nth --counter 0 --every 3 --packet 2 -j DNAT --to-destination 192.168.1.103:443`

###### Allow Ping from outside to inside:
 `# iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT`
  `# iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT`

###### Allow Ping from inside to outside:
  `# iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT`
  `# iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT`

###### Allow Loopback access:
  `# iptables -A INPUT -i lo -j ACCEPT`
  `# iptables -A OUTPUT -o lo -j ACCEPT`

###### Allow internal network to external network:
  `# iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT`

###### Allow outbound DNS:
  `# iptables -A OUTPUT -p udp -o eth0 --dport 53 -j ACCEPT`
  `# iptables -A INPUT -p udp -i eth0 --sport 53 -j ACCEPT`

###### Allow Rsync from a specific network:
  `# iptables -A INPUT -i eth0 -p tcp -s 192.168.101.0/24 --dport 873 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 873 -m state --state ESTABLISHED -j ACCEPT`

###### Allow MySQL connection only from a specific network:
  `# iptables -A INPUT -i eth0 -p tcp -s 192.168.100.0/24 --dport 3306 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 3306 -m state --state ESTABLISHED -j ACCEPT`

###### Allow Sendmail or Postfix traffic:
  `# iptables -A INPUT -i eth0 -p tcp --dport 25 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 25 -m state --state ESTABLISHED -j ACCEPT`

###### Allow IMAP:
  `# iptables -A INPUT -i eth0 -p tcp --dport 143 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 143 -m state --state ESTABLISHED -j ACCEPT`

###### Allow IMAPS:
  `# iptables -A INPUT -i eth0 -p tcp --dport 993 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 993 -m state --state ESTABLISHED -j ACCEPT`

###### Allow POP3:
  `# iptables -A INPUT -i eth0 -p tcp --dport 110 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 110 -m state --state ESTABLISHED -j ACCEPT`

###### Allow POP3S:
  `# iptables -A INPUT -i eth0 -p tcp --dport 995 -m state --state NEW,ESTABLISHED -j ACCEPT`
  `# iptables -A OUTPUT -o eth0 -p tcp --sport 995 -m state --state ESTABLISHED -j ACCEPT`

###### Prevent DoS attack:
  `# iptables -A INPUT -p tcp --dport 80 -m limit --limit 25/minute --limit-burst 100 -j ACCEPT`

###### Log Dropped Packets:
  `# iptables -N LOGGING # Create a new chain called LOGGING`
  `# iptables -A INPUT -j LOGGING # Make sure remaining incoming connections jump to the LOGGING chain`
  `# iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables Packet Dropped: " --log-level 7 # Log these packets by specifying a custom "log-prefix"`
  `# iptables -A LOGGING -j DROP # Finally, drop these packets.`

###### Port forwarding
Route all traffic that comes from port 442 to port 22:
  `# iptables -t nat -A PREROUTING -p tcp -d 192.168.102.37 --dport 422 -j DNAT --to 192.168.102.37:22``
  ``# iptables -A INPUT -i eth0 -p tcp --dport 422 -m state --state NEW,ESTABLISHED -j ACCEPT`
You will also need to allow the port you are forwarding:
``# iptables -A OUTPUT -o eth0 -p tcp --sport 422 -m state --state ESTABLISHED -j ACCEPT`