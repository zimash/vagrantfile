# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "devel.local"
  config.vagrant.plugins = ["vagrant-vbguest"]

  config.vm.network "private_network", :type => "dhcp", :adapter => 2
  config.vm.synced_folder ".", "/nfs", :type => "nfs" # require root

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
    vb.cpus = 4
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    yum install -y yum-utils device-mapper-persistent-data lvm2
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum install -y docker-ce gcc git vim make
    cd /tmp
    curl https://dl.google.com/go/go1.13.6.linux-amd64.tar.gz -o go1.13.6.linux-amd64.tar.gz
    tar -C /usr/local/ -zxf /tmp/go1.13.6.linux-amd64.tar.gz && rm /tmp/go1.13.6.linux-amd64.tar.gz
  SHELL
end
