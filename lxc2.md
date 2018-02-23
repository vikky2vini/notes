## Linux Containers (lxc2)

#### Getting started

###### Initialization (new installation)
    `lxd init`

###### List containers
    `lxc list'

###### Create a new Ubuntu container
  `lxc launch ubuntu:16.04 mycontainer`
  or:
  `lxc launch images:ubuntu/xenial mycontainer`

###### Create a new Ubuntu container (on a specific storage pool)
  `lxc launch ubuntu:16.04 mycontainer -s main`

###### Delete a container
  `lxc delete mycontainer

###### Running a command within a container
  `lxc exec <container_name> bash`

###### Login in to the container
  `lxc exec mycontainer -- sudo --login --user ubuntu`

###### Running a command which requires arguments within a container
  `lxc exec <container_name> -- ls -lh`

#### Working with profiles
###### Create a new profile
  `lxc profile create myprofile`

###### Edit a profile
  `lxc profile edit myprofile`

###### Delete a profile
  `lxc profile delete myprofile1

###### Launch a container with a specific profile:
  `lxc launch mynewcontainer -p myprofile -p extbr0`

###### Launch a container with a specific profile, and apply a second to override the first:
  `lxc launch mynewcontainer -p default -p extbr0`

###### Show the current profile configuration
  `lxc profile show extbr0`

###### Edit a network profile
  `lxc profile edit extbr0`

###### External accessible bridge example
  ```
  description: External access profile
  devices:
    eth0:
      name: eth0
      nictype: bridged
      parent: br0
      type: nic
  ```

#### Working with storage pools

###### List storage pools
  `lxc storage list`

###### Creating a new storage pool, mapped to file-system directory
  `lxc storage create main dir source=/opt/lxd`

###### Create a new storage pool, mapped to block device
  `lxc storage create pool-name btrfs source=/dev/sdb`

###### Deleting a storage pool
  `lxc storage delete main`

###### Set default storage pool
  `lxc profile edit default`
  Set the default storage volume in the editor that appears

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
