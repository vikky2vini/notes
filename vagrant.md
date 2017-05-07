## Vagrant

#### Managing boxes:

* Vagrant boxes are stored in ~/.vagrant.d
* You can add a new box with the following command:
  `$ vagrant box add <boxname>`
  Example:
  `$ vagrant box add debian/jessie64`

* List of all installed boxes:
  `$ vagrant box list`

###### Create a package:
  cd into the directory of the vagrant file and execute:
    `$ vagrant package --output packagename.box`

###### Import a package:
  `$ vagrant box add <packagename> package.box`

###### Remove a box:
  `$ vagrant box remove debian/jessie64`

###### SSH directly into a box:
From within the directory with the Vagrant file, run:
  `$ vagrant ssh`

###### Print SSH config:
From within the directory with the Vagrant file, run:
  `$ vagrant ssh-config`

###### Reprovision a VM:
Note: Normally, provision only runs one time. The following command, when executed within the directory containing the Vagrantfile, will run this step again:
  `$ vagrant provision`

#### Plugins

###### kvm
     `$ vagrant plugin install vagrant-kvm`

###### virtualbox
     `$ vagrant plugin install vagrant-vbguest`

#### Vagrant Files

###### Create a fresh vagrant file
  * Create directory (the name of the directory will become the first portion of the vm name:
    `$ vagrant init debian/jessie64`

  * Implement these parameters between the following lines of the Vagrant file:

    ```Vagrant.configure(2) do |config|
      <config goes here>
    end```

###### Declare box to use:
    $ config.vm.box = "debian/jessie64"

###### Choose a name for the VM:
Underneath config.vm.box = "ubuntu/xenial64" add:

    config.vm.define :Test1 do |t|
    end

###### Forward a port:
    $ config.vm.network "forwarded_port", guest: 80, host: 8080

###### Use a bash script to provision (store it in the same dir):
    $ config.vm.provision "shell", path: "provision.sh"

###### Public networking:
    $ config.vm.network "public_network", bridge: "eno1"

#### Working with VMs

###### Start a VM:
    $ vagrant up

###### Check status of a VM:
    $ vagrant status

###### SSH into a VM:
    $ vagrant ssh

###### Stop a VM:
    $ vagrant halt

###### Reboot a VM:
    $ vagrant reload

###### Halt and delete a VM:
    $ vagrant destroy

#### Previous issues

###### Unable to deploy a VM in Virtualbox
Insall the vagrant-vbguest package:

    
