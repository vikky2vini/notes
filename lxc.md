## Linux Containers

#### Configuration

###### Changing storage location for containers
    Edit or create the following file: /etc/lxc/lxc.conf
    Add the line: lxc.lxcpath = /opt/lxc

#### lxc commands

###### Create a new 64-bit Ubuntu container:
  `# lxc-create -t ubuntu -n mycontainer`

###### Create a new 32-bit Ubuntu container:
  `# lxc-create -t ubuntu -n mycontainer32 -- -a i686`

##### Create a container of a specific distribution release version:
  `# lxc-create -n test64 -t ubuntu -- -r xenial`

##### Create a container with a specific user name:
  ` # lxc-create -n games -t ubuntu -- --user jay -r xenial`

###### Create a container of a specific distribution release version (i686):
  `# lxc-create -n test32 -t ubuntu -- -a i686 --release xenial`

##### Create a container with rootfs in a different directory:
  `# lxc-create -n games -t ubuntu --dir /opt/lxc/games -- -r xenial`

###### Delete (destroy) a container:
  `# lxc-destroy -n test`

###### Start a container:
  `# lxc-start -n mycontainer`

###### Open a console to a container:
  `# lxc-console -n mycontainer32`

###### Run commands against a container directly from the host:
  `# lxc-attach -n mycontainer32 -- sudo apt-get update`

###### Install required packages for setting up a gaming container
  `sudo lxc-attach -n gaming-test-2 -- sudo apt-get install aptitude alsa-utils libasound2:i386 libasound2-data:i386 libasound2-plugins:i386 libc6:i386 libgl1-mesa-dev libgl1-mesa-glx:i386 libglu1-mesa:i386 libgtk2.0-0:i386 liblcms2-2:i386 libnss-mdns:i386 libsdl2-2.0-0:i386 libsdl2-image-2.0-0:i386 mesa-utils python-gtk2`

##### Additional packages requried for setting up a gaming container (nvidia):
  `# sudo lxc-attach -n gaming-test-2 -- sudo apt-get install --no-install-recommends nvidia-367 nvidia-367:i386` Note: the second package is an assumption.

###### Enable 32-bit packages in container (Debian-based):
  `sudo lxc-attach -n gaming-test-2 -- sudo dpkg --add-architecture i386`

###### Back up and restore an LXC container
  'cd /opt/lxc'
  'tar --numeric-owner -czvf games.tar.gz games'

###### Restore an LXC container
  'cd /opt/lxc'
  'tar --numeric-owner -xzvf games.tar.gz


#### Config tweaks

Note: Set these in /etc/lxc/default.conf to make them always present in the resulting container.

###### Networking
    lxc.network.type = veth
    lxc.network.link = virbr0
    lxc.network.flags = up

###### Mounting directories from the host
    lxc.mount.entry = /opt/games opt/games none bind,create=dir

###### Accessing display (X) from the host
    lxc.mount.entry = tmpfs tmp tmpfs defaults
    lxc.mount.entry = /dev/dri dev/dri none bind,optional,create=dir
    lxc.mount.entry = /tmp/.X11-unix tmp/.X11-unix none bind,optional,create=dir
    lxc.mount.entry = /dev/video0 dev/video0 none bind,optional,create=file
    lxc.cgroup.devices.allow = c 226:* rwm

###### Accessing nvidia card from the host
    Add the mount entries in the step previous.
    Install the nvidia driver: # sh <nvidia_installer>.run --no-kernel-module

    Add the following lines to the config file:
      lxc.cgroup.devices.allow = c 195:* rwm

    Add the following lines to manually moutn /dev/nvidia* devices:
      lxc.mount.entry = /dev/nvidia0 dev/nvidia0 none bind,optional,create=file
      lxc.mount.entry = /dev/nvidiactl dev/nvidiactl none bind,optional,create=file
      lxc.mount.entry = /dev/nvidia-modeset dev/nvidia-modeset none bind,optional,create=file

    Create required dev files (if not mounting /dev/nvidia* devices:
      cd /dev
      mknod -m 666 nvidia-modeset c 195 254
      mknod -m 666 nvidia0 c 195 0
      mknod -m 666 nvidiactl c 195 255

##### Accessing sound card from the host
    lxc.cgroup.devices.allow = c 116:* rwm
    lxc.mount.entry = /dev/snd dev/snd none bind,optional,create=dir
    lxc.mount.entry = ~/.config/pulse home/jay/.config/pulse none bind,optional,create=dir


#### Complete configuration example

  # Common configuration
  lxc.include = /usr/share/lxc/config/ubuntu.common.conf
  lxc.rootfs = /opt/lxc/games/rootfs
  lxc.rootfs.backend = dir
  lxc.utsname = games
  lxc.arch = amd64

  # X
  lxc.mount.entry = tmpfs tmp tmpfs defaults
  lxc.mount.entry = /dev/dri dev/dri none bind,optional,create=dir
  lxc.mount.entry = /tmp/.X11-unix tmp/.X11-unix none bind,optional,create=dir
  lxc.mount.entry = /dev/video0 dev/video0 none bind,optional,create=file
  lxc.cgroup.devices.allow = c 226:* rwm

  # Nvidia
  lxc.cgroup.devices.allow = c 195:* rwm
  lxc.mount.entry = /dev/nvidia0 dev/nvidia0 none bind,optional,create=file
  lxc.mount.entry = /dev/nvidiactl dev/nvidiactl none bind,optional,create=file
  lxc.mount.entry = /dev/nvidia-modeset dev/nvidia-modeset none bind,optional,create=file

  # Audio
  lxc.cgroup.devices.allow = c 116:* rwm
  lxc.mount.entry = /dev/snd dev/snd none bind,optional,create=dir
  lxc.mount.entry = ~/.config/pulse home/jay/.config/pulse none bind,optional,create=dir

  # Network configuration
  lxc.network.type = veth
  lxc.network.hwaddr = 00:16:3e:67:d8:17
  lxc.network.link = virbr0
  lxc.network.flags = up


#### Previous issues

###### Unable to use GUI applications
    Execute on host: xhost +
    Add to .bashrc inside the container: export DISPLAY=:0

###### Unable to play audio
    Install the following package in the container (Ubuntu): alsa-utils

###### Errors while installing Crossover
    Install the following package into the container: python-gtk2
