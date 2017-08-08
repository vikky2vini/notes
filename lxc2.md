## Linux Containers (lxc2)

#### Configuration

###### Initialization (new installation)
    `lxd init`

###### List containers
    `lxc list'

###### Create a new Ubuntu container
  `lxc launch ubuntu:16.04 mycontainer`

###### Delete a container
  `lxc delete mycontainer

###### Running a command within a container
  `lxc exec <container_name> bash`

#### Working with images

###### List image repositories
  `lxc image list`

##### List available images
  `lxc image list`

##### Retrieve information about an image
  `lxc image info <image_name>`

###### Add a new image repository
  `lxc remote add <name> <host>

##### Delete a local image
  `lxc image delete <image_name>`

###### Create an image from an existing container
  `lxc publish <container> --alias <new_image_name>

#### Configuration

###### Automatically start a container at boot
  `lxc config set <container_name> boot.autostart 1

###### Delay autostart of a container
  `lxc config set <container_name> boot.autostart.delay 30

###### Set priority (setting autostart order)
  `lxc config set <container_name> boot.autostart.order 8

#### Helpful links
https://www.jamescoyle.net/cheat-sheets/2540-lxc-2-x-lxd-cheat-sheet
