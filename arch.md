## Arch Linux

#### Misc Tweaks

###### Disable turbo boost:
  `# echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo`

###### Disable systemd from handling lid close events:
Edit `/etc/systemd/logind.conf` and set `HandleLidSwitch` to `ignore`.

###### Accessing a wifi network via the shell:
  Use `wifi-menu`. If not available, you an manually bring up a wireless info by performing the following:
  1. `#cp /etc/netctl/examples/wireless-wpa /etc/netctl/imagisphere`
  2. Edit `/etc/netctl/imagisphere` with network info
  3. `# netctl start imagisphere`

### Installation procedures
###### Installation procedure (no encryption):
  1. Partition disk, create lvm partition:

     `# fdisk /dev/sda`

      * o
      * enter
      * w
      * n
      * p
      * 1
      * enter
      * enter
      * t
      * 1
      * 8E
      * w

  2.  Create lvm:
        * Non-SSD: `# pvcreate /dev/sda1`
        * SSD: `# pvcreate --dataalignment 1m /dev/sda1`
        * Example commands for setting up LVM:
          * `# vgcreate volgroup0 /dev/sda1`
          * `# lvcreate -L 30GB volgroup0 -n lv_root`
          * `# lvcreate -L 10GB volgroup0 -n lv_swap`
          * `# lvcreate -L 250GB volgroup0 -n lv_home`
          * `# modprobe dm_mod`
          * `# vgscan`
          * `# vgchange -ay`
  3.  `# mkfs.ext4 /dev/volgroup0/lv_root`
  4.  `# mkfs.ext4 /dev/volgroup0/lv_home`
  5.  `# mount /dev/volgroup0/lv_root /mnt`
  6.  `# mkdir /mnt/home`
  7.  `# mount /dev/volgroup0/lv_home /mnt/home`
  8.  `# pacstrap -i /mnt base`
  9.  `# genfstab -U -p /mnt >> /mnt/etc/fstab`
  10.  `# arch-chroot /mnt`
  11. `# pacman -S openssh grub-bios linux-headers linux-lts linux-lts-headers`
  12. If wireless: `# pacman -S dialog wpa_supplicant wireless_tools`
  13. Edit `/etc/mkinitcpio.conf` and add `lvm2` in between `block` and `filesystems`
  14. `# mkinitcpio -p linux`
  15. `# mkinitcpio -p linux-lts`
  16. `# nano /etc/locale.gen (uncomment en_US.UTF-8)`
  17. `# locale-gen`
  18. `# ln -s /usr/share/zoneinfo/America/Detroit /etc/localtime`
  19. `# hwclock --systohc --utc`
  20. Enable `root` logon via `ssh`
  21. `# systemctl enable sshd.service`
  22. `# passwd` (for root)
  23. `# grub-install --target=i386-pc --recheck /dev/sda`
  24. `# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo`
  25. `# grub-mkconfig -o /boot/grub/grub.cfg`
  26. `$ exit`
  27. `# umount /mnt/home`
  28. `# umount /mnt`
  29. `# reboot`

###### Installation procedure (encrypted lvm):
  1. Partition disk, create boot and lvm partitions:

       `# fdisk /dev/sda`

        * n
        * p
        * 1
        * enter
        * +400M
        * n
        * p
        * 2
        * enter
        * enter
        * t
        * 2
        * 8E
        * w

  2. Set up encryption
       * `$ cryptsetup luksFormat /dev/sda2`
       * `$ cryptsetup open --type luks /dev/sda2 lvm`

  3.  Set up lvm:
        * `# pvcreate --dataalignment 1m /dev/mapper/lvm`
        * `# vgcreate volgroup0 /dev/mapper/lvm`
        * `# lvcreate -L 30GB volgroup0 -n lv_root`
        * `# lvcreate -L 10GB volgroup0 -n lv_swap`
        * `# lvcreate -L 250GB volgroup0 -n lv_home`
        * `# modprobe dm_mod`
        * `# vgscan`
        * `# vgchange -ay`

  4.  `# mkfs.ext2 /dev/sda1`
  5.  `# mkfs.ext4 /dev/volgroup0/lv_root`
  6.  `# mkfs.ext4 /dev/volgroup0/lv_home`
  7.  `# mount /dev/volgroup0/lv_root /mnt`
  8.  `# mkdir /mnt/boot`
  9.  `# mount /dev/sda1 /mnt/boot`
  10. `# mkdir /mnt/home`
  11. `# mount /dev/volgroup0/lv_home /mnt/home`
  12. `# pacstrap -i /mnt base`
  13. `# genfstab -U -p /mnt >> /mnt/etc/fstab`
  14. `# arch-chroot /mnt`
  15. `# pacman -S openssh grub-bios linux-headers linux-lts linux-lts-headers`
  16. If wireless: `# pacman -S dialog wpa_supplicant wireless_tools`
  17. Edit `/etc/mkinitcpio.conf` and add `encrypt lvm2` in between `block` and `filesystems`
  18. `# mkinitcpio -p linux`
  19. `# mkinitcpio -p linux-lts`
  20. `# nano /etc/locale.gen` (uncomment en_US.UTF-8)
  21. `# locale-gen`
  22. `# ln -s /usr/share/zoneinfo/America/Detroit /etc/localtime`
  23. `# hwclock --systohc --utc`
  24. Enable `root` logon via `ssh`
  25. `# systemctl enable sshd.service`
  26. `# passwd` (for root)
  27. Edit `/etc/default/grub`:
        add `cryptdevice=<UUID>:volgroup0` to the `GRUB_CMDLINE_LINUX_DEFAULT` line
        If using standard device naming, the option will look like this: `cryptdevice=/dev/sda2:volgroup0`
  29. `# grub-install --target=i386-pc --recheck /dev/sda`
  30. `# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo`
  31. `# grub-mkconfig -o /boot/grub/grub.cfg`
  32. `$ exit`
  33. `# umount /mnt/boot`
  34. `# umount /mnt/home`
  35. `# umount /mnt`
  36. `# reboot`
  37. Once Arch boots up, see if it has an IP address: ip addr show
  38. If not: `# dhcpcd`


###### Post installation steps:
  1. Fix GNOME app issues: `# localectl set-locale LANG="en_US.UTF-8"`
  2. Find `blkid` for swap, add it to fstab: `UUID=<UUID> none swap defaults 0 0`
  3. Add to `fstab`:
	   `tmpfs   /tmp         tmpfs   nodev,nosuid,size=2G          0  0`
  4. If ssd, add `discard` to `fstab`. Example:
	   `UUID=<UUID>	/         	ext4      	defaults,noatime,discard	0 2`


#### Previous Issues:
###### If grub gives an error on step 18, add the following to the end of /etc/default/grub:
		# Fix broken grub.cfg gen
		GRUB_DISABLE_SUBMENU=y
