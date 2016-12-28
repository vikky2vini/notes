## netctl

###### Connecting to a wireless network
 1. Create config file, and store it in:
      `/etc/netctl/<if>-<SSID>`
    Note: You can use wifi-menu to create this file.

 2. Start and enable the netctl config file:
      `# netctl start <if>-<SSID>`
      `# netctl enable <if>-<SSID>`
