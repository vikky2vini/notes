## systemd

#### Unit Commands
###### Analyzing system state:
	$ systemctl list-units

###### List failed units:
	$ systemctl --failed

###### Start, stop or restart a unit:
	# systemctl start|stop|restart unit

###### Check the status of a unit:
	$ systemctl status unit

###### Check whether or not a unit is already enabled or not:
	$ systemctl is-enabled unit

###### Enable or disable a unit:
	# systemctl enable|disable unit

###### Power management commands:
	$ systemctl reboot
	$ systemctl poweroff
	$ systemctl suspend

#### Journal commands
###### Show all messages from this boot:
	# journalctl -b

###### Follow new messages:
	# journalctl -f

###### Show all messages from a specific executable:
	# journalctl /usr/lib/systemd/systemd

###### Show all messages from a specific process:
	# journalctl _PID=1

###### Show messages from a specific unit:
	# journalctl -u unit

###### Show the kernel ring buffer:
	# journalctl _TRANSPORT=kernel