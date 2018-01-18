# Vagrant vEOS

# Build

Download vEOS-lab-4.20.1F-virtualbox.box
- https://www.arista.com/en/support/software-download

```
$ vagrant box add --name vEOS vEOS-lab-4.20.1F-virtualbox.box
```

```
$ vagrant box list

vEOS                                 (virtualbox, 0)
```

```
$ vagrant init
```

```
$ vi Vagrantfile

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define :iosxrv1 do |veos1|
    voes1.vm.box = "vEOS"
  end
end
```

```
$ vagrant up
```

```
$ vagrant status
Current machine states:

veos1                     running (virtualbox)
```

# Access and log in

```
$ vagrant ssh veos

-bash-4.3#

-bash-4.3# FastCli

localhost>

localhost>show version

Arista vEOS
Hardware version:
Serial number:
System MAC address:  0800.273e.22fd

Software image version: 4.20.1F
Architecture:           i386
Internal build version: 4.20.1F-6820520.4201F
Internal build ID:      790a11e8-5aaf-4be7-a11a-e61795d05b91

Uptime:                 3 minutes
Total memory:           2017324 kB
Free memory:            1260716 kB
```

# Default configuration

```
localhost#show running-config
! Command: show running-config
! device: localhost (vEOS, EOS-4.20.1F)
!
! boot system flash:/vEOS-lab.swi
!
event-handler dhclient
   trigger on-boot
   action bash sudo /mnt/flash/initialize_ma1.sh
!
transceiver qsfp default-mode 4x10G
!
spanning-tree mode mstp
!
aaa authorization exec default local
!
aaa root secret sha512 $6$tw6vnkVkaKdJGA0g$kev.m4/a6pkPz7eilSeF/s/ucuUt3hjhVQcVYuy5xbLHWEcK0hjYRtIiITOh0cU6i/J6spv6F7PBWYEM8qiLV.
!
username admin privilege 15 role network-admin secret sha512 $6$m.wo8pRqCQoFHgkW$xPxVgK9pn6rDKvALeHAl3lYLjbEbI2aDes1i5g5qRHAOAH6O0R/dckJ3ovAU.OXuahBIoMFTKu1WklUULGJpV0
username vagrant privilege 15 role network-admin secret sha512 $6$0FNOoFHOd6T64Vh7$ZrkHk2hRkAz/hDGeby/EM4aYDRNqKm5ebjOK3Tq8YGKv5E2gPfw5fF5CSxptKjaL55WU6AmM3ioOmC7ZR5ePr1
!
interface Management1
   ip address 10.0.2.15/24
!
no ip routing
!
management api http-commands
   no shutdown
!
end
```

# Reference
- [Using vEOS with Vagrant and VirtualBox](https://eos.arista.com/using-veos-with-vagrant-and-virtualbox/)
