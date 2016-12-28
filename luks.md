## luks

###### Create an encrypted volume:
  `# cryptsetup luksFormat /dev/sdb`

###### Format an encrypted volume:
1. `# cryptsetup luksOpen /dev/sdc backup_drive`
2. `# mkfs.ext2 -L "backup_drive" /dev/mapper/backup_drive`

###### Mounting an encrypted volume:
1. `# cryptsetup luksOpen /dev/sdb backup_drive`
2. Enter password
3. `# mount /dev/mapper/backup_drive /media/backup_drive`

###### Closing a volume:
1. `# umount /media/backup_drive`
2. `# cryptsetup luksClose /dev/mapper/backup_drive`

###### Change the passphrase:
1. `# umount /media/ext_disk`
2. `# cryptsetup luksClose /dev/mapper/backup_drive`
3. `# cryptsetup luksChangeKey /dev/sdc -S 0`

###### Change drive label:
  `# e2label /dev/mapper/luks_crypto_[UUID] [LABEL]`
