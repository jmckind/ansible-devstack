# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "devstack"

    config.vm.network "forwarded_port", guest: 80, host: 8800     # horizon
    config.vm.network "forwarded_port", guest: 5000, host: 5000   # keystone public/internal
    config.vm.network "forwarded_port", guest: 35357, host: 35357 # keystone admin
    config.vm.network "forwarded_port", guest: 8773, host: 8773   # nova ec2
    config.vm.network "forwarded_port", guest: 8774, host: 8774   # nova compute
    config.vm.network "forwarded_port", guest: 9292, host: 9292   # glance
    config.vm.network "forwarded_port", guest: 8776, host: 8776   # cinder
    config.vm.network "forwarded_port", guest: 9696, host: 9696   # neutron
    config.vm.network "forwarded_port", guest: 8777, host: 8777   # ceilometer
    config.vm.network "forwarded_port", guest: 8080, host: 8080   # swift
    config.vm.network "forwarded_port", guest: 8004, host: 8004   # heat orchestration
    config.vm.network "forwarded_port", guest: 8000, host: 8000   # heat cloud formation

    config.vm.synced_folder "stack", "/opt/stack"

    config.vm.provider "virtualbox" do |vbx|
        vbx.customize ["modifyvm", :id, "--memory", "4096"]
    end

    if Vagrant.has_plugin?("vagrant-vbguest")
        config.vbguest.auto_update = false
    end
end
