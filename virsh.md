## virsh

#### Domain commands

###### List all domains:
  `# virsh list --all` (may need sudo)

###### Start a domain:
  `# virsh start <domain> or <uuid>`

###### Start a domain and attach to console:
  `# virsh start --console <domain> or <uuid>`

###### Start a domain, attach to console, and automatically destroy when done:
  `# virsh start --console --autodestroy <domain> or <uuid>`

###### Suspend a domain:
  `# virsh suspend <domain>`

###### Resume a domain:
  `# virsh resume <domain>`

###### Reboot a domain (gracefully):
  `# virsh reboot <domain>`

###### Reboot a domain (ungracefully):
  `# virsh reset <domain>`

###### Shut down a domain (gracefully):
  `# virsh shutdown <domain>`

###### Shut down a domain (ungracefully)
  `# virsh destroy <domain>`

###### List all domains that are configured to autostart:
  `# virsh list --autostart`

###### List all domains that are NOT configured to autostart:
  `# virsh list --no-autostart`

###### Configure a domain to start automatically at boot:
  `# virsh autostart <domain>`

###### Configure a domain to NOT start automatically at boot:
  `# virsh autostart --disable <domain>`

###### Save domain state:
  `# virsh save <domain> <state-file>`

###### Restore domain state:
  `# virsh restore <state-file>`

#### Snapshots
###### Create a snapshot of a VM:
  `# virsh snapshot-create-as <domain> <snapshot_name> "<description>"`

###### List snapshots for a domain:
  `# virsh snapshot-list <domain>`

###### Restore a snapshot of a domain:
  `# virsh snapshot-revert <domain> <snapshot_name>`

###### Delete a snapshot for a domain:
  `# virsh snapshot-delete <domain> <snapshot_name>`