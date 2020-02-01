# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$SCRIPT = <<-SCRIPT
echo I am provisioning...

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

grep '192.168.76.76 vm1 vm1.vagrant' /etc/hosts \
  || cat <<EOF_ETC_HOSTS | sudo tee -a /etc/hosts

# add addresses to /etc/hosts
192.168.76.76 vm1.vagrant
192.168.76.77 vm2.vagrant
#192.168.76.78 vm3.vagrant
EOF_ETC_HOSTS

date > /etc/vagrant_provisioned_at

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "vm1" do |node|
    node.vm.box = "bento/ubuntu-18.04"
    #node.vm.hostname = "vm1.vagrant"
    node.vm.define "vm1"
    node.vm.network :private_network, ip: "192.168.76.76"
    node.ssh.insert_key = false

    node.vm.provider :virtualbox do |v|
      v.memory = 1536
      #v.name = "vm1"

      # [virtualbox configuration](https://www.vagrantup.com/docs/virtualbox/configuration.html)
      # [VBoxManage modifyvm](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm)

      #[Enabling DNS Proxy in NAT Mode](https://www.virtualbox.org/manual/ch09.html#nat-adv-dns)
      #v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]

      # [Miscellaneous Settings](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm-other)
      # Disable console log from being required
      #v.customize [ 'modifyvm', :id, '--uartmode1', 'disconnected']
    end

    node.vm.provision "shell", inline: $SCRIPT

    # Ansible provisioning.
    # Run Ansible from the Vagrant Host
    #node.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "provision.yml"
    #  ansible.inventory_path = "vagrant.inv"
    #  ansible.become = true
    #  ansible.compatibility_mode = "2.0"
    #end
  end

  config.vm.define "vm2" do |node|
    node.vm.box = "bento/ubuntu-18.04"
    #node.vm.hostname = "vm2.vagrant"
    node.vm.define "vm2"
    node.vm.network :private_network, ip: "192.168.76.77"
    node.ssh.insert_key = false

    node.vm.provider :virtualbox do |v|
      v.memory = 1536
      #v.name = "vm2"

      # [virtualbox configuration](https://www.vagrantup.com/docs/virtualbox/configuration.html)
      # [VBoxManage modifyvm](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm)

      #[Enabling DNS Proxy in NAT Mode](https://www.virtualbox.org/manual/ch09.html#nat-adv-dns)
      #v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]

      # [Miscellaneous Settings](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm-other)
      # Disable console log from being required
      #v.customize [ 'modifyvm', :id, '--uartmode1', 'disconnected']
    end

    node.vm.provision "shell", inline: $SCRIPT

    # Ansible provisioning.
    # Run Ansible from the Vagrant Host
    #node.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "provision.yml"
    #  ansible.inventory_path = "vagrant.inv"
    #  ansible.become = true
    #  ansible.compatibility_mode = "2.0"
    #end
  end
end
