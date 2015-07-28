# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "devstack"
    config.vm.network "forwarded_port", guest: 80, host: 8000
    config.vm.synced_folder "stack", "/opt/stack"

    config.vm.provider "virtualbox" do |vbx|
        vbx.customize ["modifyvm", :id, "--memory", "4096"]
    end

    if Vagrant.has_plugin?("vagrant-vbguest")
        config.vbguest.auto_update = false
    end
end
