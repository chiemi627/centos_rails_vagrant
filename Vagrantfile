# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "chef/centos-6.5"

  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :private_network, ip: "192.168.33.10"

  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true
  
  config.vm.provision "shell", inline: <<-SHELL
	sudo yum -y update kernel*
        sudo localedef -f UTF-8 -i ja_JP /usr/lib/locale/ja_JP.UTF-8
  SHELL

  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe  "apt"
    chef.add_recipe  "yum"
    chef.add_recipe  "emacs"
    chef.add_recipe  "git::default"
    chef.add_recipe  "git::source"
    chef.add_recipe  "git::windows"
    chef.add_recipe  "java"
    #chef.add_recipe "libffi"
    #chef.add_recipe "libffi::dev"
    chef.add_recipe  "ruby_build"
    chef.add_recipe  "rbenv"
    chef.add_recipe  "sqlite"
    chef.add_recipe "mysql::server"
    chef.add_recipe "mysql::client"
    chef.add_recipe "postgresql"
    chef.add_recipe "postgresql::server"
    chef.add_recipe "database::postgresql"
    chef.add_recipe "enpit"
    chef.add_recipe "enpit::github-connect"
    chef.add_recipe "enpit::generate_rails"
    chef.add_recipe "enpit::bash_profile"
    chef.add_recipe "enpit::gemrc"
    chef.add_recipe "enpit::gitconfig"
    chef.add_recipe "postgresql_setup"
    chef.add_recipe "gems"
    chef.add_recipe "golang"
    chef.add_recipe "hub"
    chef.add_recipe "rbenv-ruby"
    chef.add_recipe "vim"
    
    chef.json ={
      locale: {
        lang: "ja_JP.utf8",
        lc_all: "ja_JP.utf8"
      },
      mysql: {
        port:"3306",
        server_root_password:"vagrant",
        remove_anonymous_users:true
      },
      postgresql: {
        password: {
           postgres: "md5cae31bc247ad84a02394a8b12ff92d76"
        }
      }
	
    }
  end
end
