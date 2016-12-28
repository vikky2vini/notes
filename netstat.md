## netstat

###### List both listening and non-listening sockets:
	$ netstat -a | more

###### To do the same as above but user numbers instead of titles:
	$ netstat -an | more

###### List only listening ports:
    netstat -tulpn

###### Determining what is listening on a port:
    # fuser 4242/tcp
    # ls -l /proc/4242/exe
