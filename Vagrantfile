# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.box_version = "11.20230615.1"
  config.vm.provider "virtualbox" do |v|
    v.memory = 256
  end

  config.vm.define "ns01" do |ns01|
    ns01.vm.network "private_network", ip: "192.168.50.10", virtualbox__intnet: "dns"
    ns01.vm.network "private_network", ip: "192.168.10.10"
    ns01.vm.hostname = "ns01"
  end

  config.vm.define "ns02" do |ns02|
    ns02.vm.network "private_network", ip: "192.168.50.11", virtualbox__intnet: "dns"
    ns02.vm.network "private_network", ip: "192.168.10.11"
    ns02.vm.hostname = "ns02"
  end

  config.vm.define "client" do |client|
    client.vm.network "private_network", ip: "192.168.50.12", virtualbox__intnet: "dns"
    client.vm.network "private_network", ip: "192.168.10.12"
    client.vm.hostname = "client"
  end
  
  config.vm.define "client2" do |client2|
    client2.vm.network "private_network", ip: "192.168.50.13", virtualbox__intnet: "dns"
    client2.vm.network "private_network", ip: "192.168.10.13"
    client2.vm.hostname = "client2"
    client2.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/play.yml"
      ansible.inventory_path = "ansible/hosts"
      ansible.host_key_checking = "false"
      ansible.limit = "all"
    end

  end

end
