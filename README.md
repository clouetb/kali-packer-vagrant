# Kali-Packer-Vagrant

## Introduction

This project provides Packer and Vagrant configuration and supporting scripts for Kali Linux, to allow the creation of both standard Kali VMs and Vagrant boxes. Both VMware and Virtualbox are supported.

## Caveats
Currently this produces VMs with the kali standard credentials of `root` and `toor`. A `vagrant` user is also added, with the default insecure Vagrant SSH key and passwordless sudo access, in order to allow Vagrant to function. If you are not using Vagrant, it is *strongly* recommended that you remove the vagrant user and associated SSH key and strip the offending line from the sudoers file. Details on how these are created and added can be found in the `packer-scripts\vagrant-setup.yml` ansible playbook. 

## Requirements
* Packer - [https://www.packer.io](https://www.packer.io)
* Virtualbox - [https://www.virtualbox.org](https://www.virtualbox.org) or VMware Workstation
* A shedload of disk space
* (optionally) Vagrant - [https://www.vagrantup.com](https://www.vagrantup.com)

## Usage
To build the virtual machine for both VMware and VirtualBox, run the following command:
```packer build packer.json```

To only build one or the other
```packer build -only=vmware-iso packer.json```
```packer build -only=virtualbox-iso packer.json```

## Vagrant

To build the Vagrant box, specify the `packer-vagrant.json` config file instead.

To add the resulting Vagrant box to your local Vagrant installation, use the following command:
```vagrant box add --name kalirolling builds/virtualbox-kali.box```
The `--force` flag can be used to overwrite a previously built box with the same name.

To instantiate a VM with Vagrant using the box you've just added, change into a directory containing an appropriate `Vagrantfile` and issue the `vagrant up` command. An example `Vagrantfile` is provided as part of this project.

# Credits
The preseed configuration file is borrowed from the folks at Offensive Security, and can be found at [https://github.com/offensive-security/kali-linux-preseed](https://github.com/offensive-security/kali-linux-preseed).