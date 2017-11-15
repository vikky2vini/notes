## Ubuntu

###### Setup live-patch service:
  1. Fully update system, reboot
  2. `# snap install canonical-livepatch`
  3. `# canonical-livepatch enable <secret_key>`
  4. Run `# canonical-livepatch status` to see status

###### Compiling mednafen:
  1. Download latest mednafen source:
	    http://sourceforge.net/projects/mednafen/
  2. `# apt-get install build-essential pkg-config libasound2-dev libcdio-dev libsdl1.2-dev libsdl-net1.2-dev libsndfile1-dev zlib1g-dev`

  3. Compile and install:
	`$ ./configure && make && sudo make install`

###### Handling display switching in MATE (docking station):
	# xrandr --output LVDS1 --off --output HDMI1 --auto --output VGA1 --auto --same-as LVDS1

###### Fix blank TTY's (occurred in Ubuntu GNOME)
Run the following commands:
  `# sed -i -e 's/#GRUB_TERMINAL/GRUB_TERMINAL/g' /etc/default/grub`
  `# update grub`

###### Make performance reasonable in Virtualbox:
1. Insert guest additions CD
2. `# apt-get install build-essential linux-headers-$(uname -r)`
3. `# ./VBoxLinuxAdditions.run`
4. Add "vboxvideo" to the end of /etc/modules
5. Reboot
