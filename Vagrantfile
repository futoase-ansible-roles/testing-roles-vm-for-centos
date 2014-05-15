# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

BENTO_CENTOS = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "CentOS-6.5-x86_64-by-opscode"
  config.vm.box_url = BENTO_CENTOS
  config.vm.box_check_update = false
  
  config.vm.network "private_network", ip: "192.168.33.33"

  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--memory", "384"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "site.yml"
    ansible.limit = "all"
    ansible.inventory_path = "vagrant.box"
    ansible.verbose = "vvvv"
  end

end
