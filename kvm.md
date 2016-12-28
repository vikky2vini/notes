## kvm

#### Installation procedure:
 * Install packages:
    * Arch-based systems:
        `# pacman -S bridge-utils libvirt qemu virt-manager ebtables dnsmasq`
    * `# yaourt virt-top`

    * Debian-based systems:
	    `# apt-get install bridge-utils libvirt-bin qemu-kvm qemu-system virt-manager virt-top virtinst`


 * Enable libvirtd (if systemd):
      `# systemctl enable libvirtd`
      `# systemctl start libvirtd`


 * Configure authentication:
	/etc/libvirt/libvirtd.conf:
		unix_sock_group = "kvm"
		unix_sock_ro_perms = "0777"  # set to 0770 to deny non-group libvirt users
		unix_sock_rw_perms = "0770"
		auth_unix_ro = "none"
		auth_unix_rw = "none"


 * Add user to kvm group:
		usermod -aG kvm <user>


 * Configure storage:
	`mkdir -p /vm_store/kvm`
	`mkdir -p /vm_store/iso_images`
	`chown root:kvm /vm_store/kvm`
	`chown root:kvm /vm_store/iso_images`
    `chmod g+w /vm_store/kvm`
    `chmod g+w /vm_store/iso_images`
	`Launch virt-manager, so that it will create /etc/libvirt/storage/default.xml`

	* Edit /etc/libvirt/storage/default.xml and set <path> to /vm_store/kvm.
	* en up virt-manager, create "iso" storage group for iso images, point it to /vm_store/iso_images.

#### Commands
###### Check status of network:
    # virsh net-list --all

#### Tweaks
###### bridge-enabled interfaces file for Debian systems:
    source /etc/network/interfaces.d/*

    # The loopback network interface
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet manual

    auto br0
    iface br0 inet dhcp
        bridge_ports eth0
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0


###### Example for setting host to use bridged networking (/etc/libvirt/qemu/vm_name.xml):
     <interface type='bridge'>
        <mac address='52:54:00:a5:41:c2'/>
        <source bridge='br0'/>
        <model type='rtl8139'/>
        <address type='pci' domain='0x0000' bus='0x00' slot='0x03' function='0x0'/>
    </interface>


#### Previous issues:
###### "Out of memory" error when creating the default network interface:
	Had to install ebtables

###### If you get an error about the file exists in regards to virbr0:
    # ip link set dev virbr0 down
    #  brctl delbr virbr0
