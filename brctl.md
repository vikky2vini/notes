## brctl

###### Delete a bridge
  `# brctl delbr br0`
   If it complains that it's still up, do this:
  `# ip link set br0 down`
