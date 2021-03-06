# Vagrant VM with Ansible

This project spins up a VM with Ansible installed, and then you can run a local Ansible playbook which will be run on the local machine.

## Quick Start Guide

### 1 - Install dependencies (VirtualBox, Vagrant, Ansible)

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).
  3. [Mac/Linux only] Install [Ansible](http://docs.ansible.com/intro_installation.html).

Note for Windows users: *This guide assumes you're on a Mac or Linux host. Windows hosts are unsupported at this time.*

### 2 - Build the Virtual Machine

  1. Download this project and put it wherever you want.
  2. Open Terminal, cd to this directory (containing the `Vagrantfile` and this REAMDE file).
  3. Run `ansible-galaxy install -r requirements.yml` to install required Ansible roles.
  4. Type in `vagrant up`, and let Vagrant do its magic.

Note: *If there are any errors during the course of running `vagrant up`, and it drops you back to your command prompt, just run `vagrant provision` to continue building the VM from where you left off. If there are still errors after doing this a few times, post an issue to this project's issue queue on GitHub with the error.*

### 3 - Configure your host machine to access the VM

  1. [Edit your hosts file](https://support.rackspace.com/how-to/modify-your-hosts-file/), adding the line `192.168.76.76  vm1.vagrant` so you can connect to the VM.
  2. Open your a terminal with `vagrant ssh vm1` so you will be connected to the VM.

  3. `sudo hostnamectl set-hostname vm1.vagrant` will be sometime helpful to set the fully qualified domain name of vm1.
  4. Then `netcat -v -w 5 vm1.vagrant 22` should return into stdout the message of a connection to the `vm1.vagrant` ssh server port:

  ```
  Connection to vm1.vagrant 22 port [tcp/ssh] succeeded!
  SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3
  ```

## Notes

- To shut down the virtual machine, enter `vagrant halt` in the Terminal in the same folder that has the `Vagrantfile`. To destroy it completely (if you want to save a little disk space, or want to rebuild it from scratch with `vagrant up` again), type in `vagrant destroy`.
