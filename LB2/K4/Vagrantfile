# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "mysql" do |web|
      web.vm.box = "ubuntu/xenial64"
      config.vm.provision :shell, inline: <<-SHELL 
      sudo apt-get update
      sudo apt-get -y install debconf-utils
      sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password admin'
	    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password admin'
      sudo apt-get -y install mysql-server
      sudo sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf
      mysql -uroot -pS3cr3tp4ssw0rd <<%EOF%
        CREATE USER 'root'@'0.0.0.0' IDENTIFIED BY 'admin';
      	GRANT ALL PRIVILEGES ON *.* TO 'root'@'0.0.0.0';
	      FLUSH PRIVILEGES;
%EOF%
      sudo service mysql restart
      sudo apt-get -y install apache2 
      sudo apt-get -y install php libapache2-mod-php php-curl php-cli php-mysql php-gd mysql-client 
      sudo mkdir /usr/share/adminer
    	sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/latest.php
	    sudo ln -s /usr/share/adminer/latest.php /usr/share/adminer/adminer.php
	    echo "Alias /adminer.php /usr/share/adminer/adminer.php" | sudo tee /etc/apache2/conf-available/adminer.conf
	    sudo a2enconf adminer.conf 
	    sudo service apache2 restart 
      sudo apt-get install ufw
      sudo ufw allow 1234/tcp
      sudo ufw allow 22/tcp
      sudo ufw allow out 22/tcp 
      sudo ufw enable
      sudo apt-get -y install openssh-server
      sudo apt-get -y install libapache2-mod-proxy-html
      sudo apt-get -y install libxml2-dev
      sudo a2enmod proxy
      sudo a2enmod proxy_html
      sudo a2enmod proxy_http
      sudo service apache2 restart
      sudo groupadd admin
      sudo useradd user01 -g admin -m -s /bin/bash 
      sudo useradd user02 -g admin -m -s /bin/bash 
      sudo chpasswd <<<user01:1234	
      sudo chpasswd <<<user02:1234
      sudo apt-get -y install unzip
      wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
      unzip ngrok-stable-linux-amd64.zip
      ./ngrok authtoken znJsMkTvBtmru1d1zvRf_4indT3cjMiW4nj7Vda32G
      ./ngrok http 1234
SHELL
      web.vm.hostname = "srv-sql"
      web.vm.network :forwarded_port, guest: 8080, host: 8080
      web.vm.network :forwarded_port, guest: 80, host: 1234
      web.vm.network "public_network", bridge: "en0: WLAN (AirPort)"
end 
 

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"

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
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
