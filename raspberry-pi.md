## Raspberry Pi Tweaks

###### Update for new pi model (warning - may include beta firmware):
Before moving to new Pi:
  `apt-get update && apt-get dist-upgrade`
  `sudo wget https://raw.github.com/Hexxeh/rpi-update/master/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update`
  `sudo rpi-update`

###### Force HDMI every boot
  Edit `/boot/config.txt`:
  Add these lines:
    `#Always force HDMI output and enable HDMI sound`
    `hdmi_force_hotplug=1`
    `hdmi_drive=2`

###### Revert back to the latest supported stable kernel/bootcode:
  `sudo apt-get update; sudo apt-get install --reinstall raspberrypi-bootloader raspberrypi-kernel`


###### Fix date and time:
  `Create symbolic link: ln -s /usr/share/zoneinfo/America/Detroit /etc/localtime`
