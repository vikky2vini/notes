## Logical Volume Manager

###### Resize a volume:
  1. Verify there is enough space:
       `# vgs`
  2. Extend the logical volume:
       `# lvextend -L +40g -n /dev/mapper/volgroup0-lv_home`
  3. Resize the file-system:
       `# resize2fs /dev/mapper/volgroup0-lv_home`

###### Create a new logical volume
       `# lvcreate -L 50GB -n lv_opt /dev/mapper/volgroup0`
       `# mkfs.ext4 /dev/mapper/volgroup0-lv_opt`

###### Take a snapshot:
  1. Verify how much space is remaining:
       `# vgs`
  2. Create the snapshot:
       `# lvcreate -L 5GB -s -n root_snapshot_20160908 /dev/mapper/volgroup0-lv_root`
  3. List current snapshots:
     `$ lvs`

###### Revert to the snapshot:
  `# lvconvert --merge /dev/volgroup0/root_snapshot_20160908`
  `# reboot`

###### Remove a snapshot (makes changes in the snapshot permanent):
  `# lvremove /dev/volgroup0/root_snapshot_20160908`
