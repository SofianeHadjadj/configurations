# -*- mode: ruby -*-
# vi: set ft=ruby :

# le vagrantfile est ecrit en Ruby

Vagrant.configure("2") do |config|

config.vm.define "osp" do |osp|

  osp.vm.box = "bento/centos-7.4"

  osp.vm.box_check_update = false

  osp.vm.network "private_network", ip: "192.168.33.10"

  osp.vm.provider "virtualbox" do |vb|

     vb.name = "osp"
     vb.memory = "2048"
  end

  # à l'interrieur de provision j'entre les commandes selon l'os (ex : yum pour centos)
  # la provision se fait en SHELL
  osp.vm.provision "shell", inline: <<-SHELL
    sudo yum install -y epel-release
    sudo yum install -y vim
    sudo yum install -y mariadb-server mariadb
    sudo yum install -y nodejs   
    sudo yum install -y httpd

    sudo systemctl start httpd
    sudo systemctl enable httpd
    sudo systemctl start mariadb
    sudo systemctl enable mariadb

    sudo npm install -g pm2
    sudo npm install -g @angular/cli
  SHELL

  osp.vm.synced_folder "C:/Users/HADJADJS/projects/osp", "/var/www/html/osp", owner: "apache", group: "apache"

end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.

end