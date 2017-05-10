## tcpdump

###### Display available interfaces
    # tcpdump -D

###### Capture packets from a specific interface
    # tcpdump -i eth0

###### Capture only N number of packets
    # tcpdump -c 5 -i eth0

###### Capture only TCP packets
    # tcpdump -i eth0 tcp

###### Capture packets, but don't convert IP addresses and port numbers to names
    # tcpdump -n -i eth0

###### Capture packets from specific source IP
    # tcpdump -i eth0 src 192.168.0.2

###### Capture packets from specific destination IP
    # tcpdump -i eth0 dst 50.116.66.139

###### Capture packets from a specific port
    # tcpdump -i eth0 port 22

###### Print captured packets in ASCII
    # tcpdump -A -i eth0

###### Print captured packets in Hex and ASCII
    # tcpdump -XX -i eth0

###### Capture and save packets in a file
    # tcpdump -w 0001.pcap -i eth0

###### Read captured packets from file
    # tcpdump -r 0001.pcap

###### Listen to Network Traffic by port:
    # tcpdump -n -nn -tttt -i eth0 port 53
