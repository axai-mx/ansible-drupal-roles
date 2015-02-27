# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty32"
# nginx config is set to allow range 192.168.0.0/16
  config.vm.network "private_network", ip: "192.168.0.8"
  #config.vm.network "forwarded_port", guest: 80, host: 8080

# set this up if you need your ssh key to clone a git repo
  #config.ssh.forward_agent = true

# set up sync folder (you need to install nfs on linux, mac already has it)
# on ubuntu the package is nfs-kernel-server
# windows does not support nfs, you'll need to remove this type
  config.vm.synced_folder "www/", "/var/www", type: "nfs"
 
  config.vm.provider "virtualbox" do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
  end
end
