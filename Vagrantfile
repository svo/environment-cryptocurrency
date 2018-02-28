# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

unless Vagrant.has_plugin?("vagrant-cachier")
  puts "Install vagrant-cachier"
  exec 'vagrant plugin install vagrant-cachier && vagrant up'
end

unless Vagrant.has_plugin?("vagrant-vbguest")
  puts "Install vagrant-vbguest"
  exec 'vagrant plugin install vagrant-vbguest && vagrant up'
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.hostname = "vagrant-cryptocurrency"
  config.vm.network :private_network, type: "dhcp"

  config.vm.provision "shell", inline: "sudo apt-get -y update && sudo apt-get -y upgrade && sudo apt-get -y install xubuntu-desktop ansible"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

  config.vm.provider :virtualbox do |vb|
    vb.memory = 4096
    vb.cpus = 2
    vb.gui = true
  end
end
