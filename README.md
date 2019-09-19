# flash-to-kubernetes-on-raspi
how to come from flash-card to kubernetes on a bunch of raspberry pi's

## Goal
I want to build an ansible project that is able to configure and update raspberry pi's from bare metal to a running kubernetes cluster.

## Editing
I use the Windows Subsystem for Linux (WSL) with debian installed. There I use vi as editor and ansible-lint to check the ansible files.

## Environment
    $ sudo apt-get update && sudo apt-get -y upgrade
    $ sudo apt-get -y install python-pip python-dev libffi-dev libssl-dev wget ssh git sshpass
    $ sudo pip install ansible
    $ sudo mkdir /etc/ansible
    $ sudo wget https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg -O "/etc/ansible/ansible.cfg"
    $ sudo pip install ansible-lint
    $ ssh-keygen -b 4096 rsa
this installs:
- ansible >= 2.7
- wget
- git
- ssh with key in .ssh/id_rsa and .ssh/id_rsa.pub
- sshpass

## Installation
clone project from github

## Quick Start
- download newest Hypriot OS
- unzip and write it to flash-card (either with flash tool or Win32 Disk Imager)
- boot raspberry pi with flash-card inserted
- copy .ssh/id_rsa.pub to raspi with
---
    $ ssh-copy-id pirate@black-pearl
---
- and password "hypriot"
- dive into ansible directory
---
    $ ansible-playbook -e dbs_hostname=node3 bootstrap.yml
---
- raspi will be configured and rebooted, then it will be accessible with
---
    $ ssh pirate@node3
---
