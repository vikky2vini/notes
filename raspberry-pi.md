## Raspberry Pi Tweaks

###### Update for new pi model (warning - may include beta firmware):
Before moving to new Pi:
  `apt-get update && apt-get dist-upgrade`
  `sudo wget https://raw.github.com/Hexxeh/rpi-update/master/rpi-update -O /usr/bin/rpi-update && sudo chmod +x /usr/bin/rpi-update`
  `sudo rpi-update`

###### Revert back to the latest supported stable kernel/bootcode:
  `sudo apt-get update; sudo apt-get install --reinstall raspberrypi-bootloader raspberrypi-kernel`


###### Fix date and time:
  `Create symbolic link: ln -s /usr/share/zoneinfo/America/Detroit /etc/localtime`
