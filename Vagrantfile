# -*- mode: ruby -*-
# vi: set ft=ruby :


####tuika sita####
def install_plugin(plugin)
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end
# Specify the required plug-in
install_plugin('vagrant-vbguest')
install_plugin('vagrant-proxyconf')
install_plugin('vagrant-docker-compose')
install_plugin('vagrant-disksize')

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  ####henkou sita####
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
    ####comment out kaijo sita####
    config.vm.box_check_update = false
  
  ####tuika sita####
  # Use the same ssh key for guest connection, considering that the distribution environment will be the same
  config.ssh.insert_key = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
    ####comment out kaijo sita####
    config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
    ####henkou sita####
    config.vm.synced_folder "./docker", "/vagrant/docker"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
    config.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false
      
      ####tuika sita####
      vb.name = "test_vm"
      vb.cpus = 4
   
      # Customize the amount of memory on the VM:
      vb.memory = "2048"
      
      ####tuika sita####
      vb.customize [
        "modifyvm", :id,
        "--clipboard", "bidirectional",
        "--draganddrop", "bidirectional",
      ]
    end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
    ####tuika sita####
    config.vm.provision :docker, run: "always"
    
  # --- Setting docker-compose. Now you can use docker-compose command in guest OS ---
  # ÅE If you don't specify a version, it will become an old version (1.11.2).
  # ÅE 1.24.0 is the latest as of March 29, 2019
  # ÅE If you want to do docker-compose up at vagrant up,
  # Remove the # in the middle of the line and enable the yml option and enter the path to docker-compose.yml
  config.vm.provision :docker_compose,
    yml: "/vagrant/docker/docker-compose.yml",
    compose_version: "1.24.1",
    run: "always"
  #end
  
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
