# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box_url = "https://Vagrantcloud.com/ubuntu/trusty64"
  config.vm.box = "ubuntu/xenial64"

  config.vm.hostname = "vagrant-cryptocurrency"
  config.vm.network :private_network, type: "dhcp"

  config.vm.provision "shell", inline: "sudo apt-get -y update && sudo apt-get -y upgrade && sudo apt-get -y install ubuntu-desktop && echo 'autologin-user=ubuntu' | sudo tee -a /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf && sudo apt-get -y install build-essential libssl-dev libffi-dev python-dev python-pip && pip install --upgrade pip && pip install ansible==2.1.1.0"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.tags = "cryptocurrency"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
end
