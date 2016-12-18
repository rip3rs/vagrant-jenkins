# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  config.vm.box_check_update = true

  config.vm.network "private_network", ip: "192.168.33.99"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.provider "virtualbox" do |vb|
    # Name the box
    vb.name = "Jenkins box"

    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  config.vm.provision "shell", inline: <<-SHELL

    PAGE_CONF="jenkins.local.dev"

    # Shell Script
    echo "##########################################"
    echo "#            ADDING REPOS                #"
    echo "##########################################"
    echo " "
    sudo add-apt-repository ppa:openjdk-r/ppa
    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    echo 'deb https://pkg.jenkins.io/debian-stable binary/' | tee -a /etc/apt/sources.list
    echo " "
    echo " "

    echo "##########################################"
    echo "#            APT-GET UPDATE              #"
    echo "##########################################"
    echo " "
    sudo apt-get -y update && sudo apt-get -y upgrade
    echo " "
    echo " "

    echo "##########################################"
    echo "#             GIT & UNZIP                #"
    echo "##########################################"
    echo " "
    sudo apt-get install -y git unzip
    echo " "
    echo " "

    echo "##########################################"
    echo "#          PYTHON SOFT JDK7              #"
    echo "##########################################"
    echo " "
    sudo apt-get install -y git unzip python-software-properties openjdk-7-jdk
    echo " "
    echo " "

    echo "##########################################"
    echo "#          JENKINS install               #"
    echo "##########################################"
    echo " "
    apt-get install -y jenkins
    sudo service jenkins start
    echo " "
    echo " "

    echo "##########################################"
    echo "#            NGINX INSTALL               #"
    echo "##########################################"
    echo " "
    sudo apt-get install -y nginx
    sudo update-rc.d nginx defaults
    echo " "
    echo " "

    echo "##########################################"
    echo "#        Making the directory            #"
    echo "##########################################"
    echo " "
    sudo mkdir -p /var/www/$PAGE_CONF
    sudo chown -R vagrant:vagrant /var/www/$PAGE_CONF
    echo " "
    echo " "

    echo "##########################################"
    echo "#          Setup Nginx hosts             #"
    echo "##########################################"
    echo " "
    cp /vagrant/config/nginx/$PAGE_CONF /etc/nginx/sites-available/
    echo "cp /vagrant/config/nginx/$PAGE_CONF /etc/nginx/sites-available/"
    echo "Copied!"
    echo " "
    echo " "

    echo "##########################################"
    echo "#            Enable Sites                #"
    echo "##########################################"
    echo " "
    sudo ln -s /etc/nginx/sites-available/$PAGE_CONF /etc/nginx/sites-enabled/
    echo " "
    echo " "

    echo "##########################################"
    echo "#            Restart Nginx               #"
    echo "##########################################"
    echo " "
    echo "Restarting Nginx."
    sudo service nginx restart
    echo " "
    echo " "

    echo "##########################################"
    echo "#   Setup direct path to working folder  #"
    echo "##########################################"
    echo " "
    echo "cd /var/www/$PAGE_CONF" >> /home/vagrant/.bashrc
    echo "cd /var/www/$PAGE_CONF" >> /home/vagrant/.bashrc
    echo " "
    echo " "

    netstat -plntu

    echo "##########################################"
    echo "#   Vagrant UP is complete!11oneeleven   #"
    echo "##########################################"

  SHELL

end
