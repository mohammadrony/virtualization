Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-stream-9"
  config.vm.box_check_update = false
  
  user = "vbox"
  subnet = "192.168.56.0"
  netmask = "255.255.255.0"

  # Define the nodes
  nodes = [
    { :name => "centos-9", :ip => "192.168.56.2" },
  ]

  # Provision each node
  nodes.each do |node|
    config.vm.define node[:name] do |config|
      config.vm.hostname = node[:name]

      config.vm.network "public_network", bridge: ["wlp0s20f3", "wlp2s0", "enp3s0"]
      config.vm.network "private_network", ip: node[:ip], subnet: subnet, netmask: netmask

      config.vm.disk :disk, size: "20GB", primary: true

      config.vm.provider "virtualbox" do |vb|
        vb.name = node[:name]
        vb.memory = 2048
        vb.cpus = 2
      end

      config.vm.provision "shell", inline: <<-SHELL
        useradd -m -s /bin/bash -p $(openssl passwd -1 #{user}) #{user}
        usermod -aG sudo #{user}
        # dnf install -y vim nmap net-tools
      SHELL
    end
  end
end
