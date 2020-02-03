# -*- mode: ruby -*-
# vi: set ft=ruby :

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
  config.vm.box = "ubuntu/xenial32"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

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
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'ESP', '--vendorid', '0x1a86', '--productid', '0x7523']
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", privileged:false, inline: <<-SHELL
    sudo apt-get update

  ## System setup
  # Step 1. https://docs.espressif.com/projects/esp-idf/en/latest/get-started/linux-setup.html
  sudo apt-get install -y git wget flex bison gperf python python-pip python-setuptools python-serial python-click python-cryptography python-future python-pyparsing python-pyelftools cmake ninja-build ccache libffi-dev libssl-dev libncurses-dev linux-image-extra-virtual

  # Step 2. https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html#get-started-get-esp-idf
  mkdir ~/esp && cd ~/esp
  
  ## ESP8266
  # Toolchain setup : https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/linux-setup.html
    
  cd ~/esp
  wget https://dl.espressif.com/dl/xtensa-lx106-elf-linux32-1.22.0-100-ge567ec7-5.2.0.tar.gz
  tar -xzf xtensa-lx106-elf-linux32-1.22.0-100-ge567ec7-5.2.0.tar.gz

  echo 'export PATH="$PATH:$HOME/esp/xtensa-lx106-elf/bin"' >> ~/.profile
  echo 'export IDF_PATH=~/esp/ESP8266_RTOS_SDK' >> ~/.profile

  export PATH="$PATH:$HOME/esp/xtensa-lx106-elf/bin"
  export IDF_PATH=~/esp/ESP8266_RTOS_SDK

  # SDK : https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/index.html#get-started-get-esp-idf
  cd ~/esp
  git clone --recursive https://github.com/espressif/ESP8266_RTOS_SDK.git

  # USB
  sudo usermod -a -G dialout $USER

  # Python requirements
  pip install --upgrade pip

  pip install --user -r $IDF_PATH/requirements.txt

  cp -r $IDF_PATH/examples/get-started/hello_world ~/esp

  SHELL

  #config.vm.provision :reload

  config.vm.provision "shell", privileged:false, inline: <<-SHELL
    pip install --user -r $IDF_PATH/requirements.txt
  SHELL


end
