# flash-to-kubernetes-on-raspi
how to come from flash-card to kubernetes on a bunch of raspberry pi's

## goal
I want to build an ansible project that is able to configure and update raspberry pi's from bare metal to a running kubernetes cluster.

## preliminaries
- I use a fritz!box as entrypoint to the internet and it's DHCP server provides IP-Adresses and delivers them if I query with nslookup and the hostname. So I can use the hostname to get the connection to new hosts.
- My raspberry pi's are of version 3 B+ and I want to flash them with Hypriot-OS (have a look at the site of hypriot on git). The result is a raspberry pi that is reachable with "ssh pirate@black-pearl.local".
- I have a Windows 10 Machine with WSL and Debian Linux running under WSL, so I have to write the latest image with Win32 Disk Imager to the flash-card and cannot use the flash utility.
- Add only one raspi to the project at the time.
- If no cluster exists, then create one and make the first one to the master node.
- If cluster exists, add next raspi to the cluster as a worker node.

## steps
1. create branch "bootstrap" for the next steps
1. create a tree for the ansible project
1. boot raspi with micro-sd card and connect to it
1. rename it with next node number and let it only be accessible with ssh-key

## Usage
1. flash micro-sd card with the newest hypriot os
1. boot raspi with micro-sd card
1. cd <to your .ssh directory>
---
$ ssh-copy-id pirate@black-pear
  enter password hypriot
---
1. cd <to your ansible directory>
---
$ ansible-playbook -e dbs_hostname=node3 bootstrap.yml
---

