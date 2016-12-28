## ufw

###### Enable ufw:
  `# ufw enable`

###### Disable ufw:
  `# ufw disable`

###### Verify ufw is running:
  `# ufw status verbose`

###### Allow a port:
  `# ufw allow 22`

###### Allow a port (TCP only):
  `# ufw allow 22/tcp`

###### Allow a port, and add a comment for the rule:
  `# ufw allow 53 comment 'open tcp and udp port 53 for dns'`

###### Deny access to a port:
  `# ufw deny 80`

###### Deny access from an IP address:
  `# ufw deny from 1.2.3.4`

###### Deny access from a subnet:
  `# ufw deny from 123.45.67.89/24`

###### Reject a port (user sees output that they are blocked, but they don't see comment):
  `# ufw reject 1194 comment 'No more vpn traffic'`

###### Allow a port range:
  `# ufw allow 6660:6670/tcp`
  `# ufw allow 6660:6670/ucp`

###### Allow a specific IP address:
  `# ufw allow from 192.168.1.106`

###### Allow a subnet:
  `# ufw allow from 192.168.1.1/24`

###### Allow access to a port from a specific IP address:
  `# ufw allow from 192.168.1.106 proto tcp to any port 22`

##### Allow access to a port from a specific subnet:
  `ufw allow from 172.16.248.0/21 to any port 22000 proto tcp comment 'Syncthing'`

###### Allow incoming traffic to a specific port:
  `# ufw allow to any port 80`

###### Delete a rule:
  `# ufw status numbered
  `# ufw delete <number>`

###### Turn off ufw (without deleting rules):
  `# ufw disable`

###### Turn off ufw and delete all the rules:
  `# ufw reset`
