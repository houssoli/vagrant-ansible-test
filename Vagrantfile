# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$SCRIPT = <<-SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at

mkdir -p /datadrive

#export DEBIAN_FRONTEND=noninteractive
#apt-get update &&
#  #apt-get -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::="--force-confold" upgrade -q -y --force-yes &&
#  apt -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::="--force-confold" dist-upgrade -q -y --force-yes
#apt install python-pip python3-pip -y
#pip3 install ansible
#python get-pip.py
#apt autoremove -y
#apt autoclean -y

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.hostname = "vm1"
  config.vm.define "vm1"
  config.vm.network :private_network, ip: "192.168.76.76"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 1536
  end

  config.vm.provision "shell", inline: $SCRIPT

  # Ansible provisioning.
  # Run Ansible from the Vagrant Host
  #config.vm.provision "ansible" do |ansible|
  #  ansible.playbook = "provision.yml"
  #  ansible.inventory_path = "vagrant.inv"
  #  ansible.become = true
  #  ansible.compatibility_mode = "2.0"
  #end
end
