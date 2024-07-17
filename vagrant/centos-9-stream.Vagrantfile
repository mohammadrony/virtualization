# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-stream-9"
  config.vm.box_check_update = false

  # Define the nodes
  nodes = [
    { :name => "node-1", :ip => "192.168.56.111" },
    { :name => "node-2", :ip => "192.168.56.112" }
  ]

  # Provision each node
  nodes.each do |node|
    config.vm.define node[:name] do |config|
      config.vm.hostname = node[:name]
      config.vm.network "private_network", ip: node[:ip]

      config.vm.provider "virtualbox" do |vb|
        vb.name = node[:name]
        vb.memory = 2048
        vb.cpus = 2
      end

      config.vm.disk :disk, size: "20GB", primary: true

      config.vm.provision "shell", inline: <<-SHELL
        # Update system
        dnf update -y

        # Install basic packages
        dnf install -y vim net-tools tcpdump nmap iptables-services
      SHELL
    end
  end
end
