## mdadm

###### Narrowing down the failed drive (at least one should provide the info):
  `# hdparm -i /dev/sdX`
  `# hwinfo --disk`
  `# smartctl -i /dev/sda`
  `# lshw -class disk`

###### Steps to replace a failed drive:
  1. Install grub on the working drive
  2. `# sfdisk -d /dev/sdb | sfdisk /dev/sda`
  3. `# mdadm --manage /dev/md0 --add /dev/sda1`

[Useful article](From: http://www.kernelhardware.org/replacing-failed-raid-drive/)
