Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"  
  
  user = "vbox"
  subnet = "192.168.56.0"
  netmask = "255.255.255.0"

  nodes = [
    { :name => "ubuntu-24", :ip => "192.168.56.2" },
  ]

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
        # apt install -y vim nmap net-tools
      SHELL
    end
  end
end
