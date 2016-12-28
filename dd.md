# dd

###### Remove MBR from a flash drive:
  `# dd if=/dev/zero of=/dev/xxx bs=446 count=1`

###### Remove the partition table from a flash drive:
  `# dd if=/dev/zero of=/dev/xxx bs=512 count=1`

###### Backup an SD card to an image:
  `# dd if=/dev/sdb of=sd.img bs=4M`

###### Restore an SD card from an image:
  `# dd if=sd.img of=/dev/sdb bs=4M`

###### Clone a hard disk to another hard disk:
  `# dd if=/dev/sda of=/dev/sdb bs=4096 conv=noerror,sync`

###### Clone partitions:
  `# dd if=/dev/sda1 of=/dev/sdb1 bs=4096 conv=noerror,sync`

###### Clone a hard disk to an image (and compress it):
  `# dd if=/dev/sda conv=sync,noerror bs=4096 | gzip -c > /path/to/my-disk.img.gz`

###### Restore from a compressed dd image:
  `# gzip –dc my-image.img.gz | dd of=/dev/sda`

###### Clone a hard disk to a remote machine:
  `# dd if=/dev/da0 conv=sync,noerror bs=4096 | gzip -c | ssh jay@server dd of=myimage.img.gz`

###### Create an ISO image of a CD or DVD:
  `# dd if=/dev/sr0 of=mydisc.iso bs=2048 conv=noerror,sync`