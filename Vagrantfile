# -*- mode: ruby -*-
# vi: set ft=ruby :

#
# Stack Username
#
$stack_username = "stack"

#
# Source directory
#
# This is where the source code for the various OpenStack projects will live.
# If you change the system user from "stack" to something else, you will need to
# update this to point at the home directory for that user.
#
$src_dir = "/opt/stack"

#
# Deployer keys
#
# This is the keypair to use for SSH connections into the instance as root.
# if you change this to a different private/public key, you will also need to update the
# ansible hosts file to use the corresponding private key.
#
$deployer_private_key = "~/.ssh/id_rsa"
$deployer_public_key = "~/.ssh/id_rsa.pub"

$bootstrap_script = <<SCRIPT
mkdir -p /root/.ssh
chmod 700 /root/.ssh
touch /root/.ssh/authorized_keys
chmod 600 /root/.ssh/authorized_keys
cat /home/vagrant/.ssh/deployer.pub >> /root/.ssh/authorized_keys

export STACK_USER=stack
useradd -s /bin/bash -m $STACK_USER

mkdir -p /home/$STACK_USER/.ssh
chmod 700 /home/$STACK_USER/.ssh
touch /home/$STACK_USER/.ssh/authorized_keys
chmod 600 /home/$STACK_USER/.ssh/authorized_keys
chown -R $STACK_USER: /home/$STACK_USER
cat /home/vagrant/.ssh/deployer.pub >> /home/$STACK_USER/.ssh/authorized_keys
SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # See (https://github.com/mitchellh/vagrant/issues/1673)

    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "osdev"

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

    config.vm.provider "virtualbox" do |vbx|
        vbx.name = "osdev"
        vbx.memory = 4096
        vbx.cpus = 4
    end

    config.vm.provision "file", source: $deployer_public_key, destination: "~/.ssh/deployer.pub"
    config.vm.provision "shell", inline: $bootstrap_script

    if File.exists?(".vagrant/machines/default/virtualbox/action_provision")
        config.ssh.username = $stack_username
        config.ssh.private_key_path = $deployer_private_key
        config.vm.synced_folder "stack", $src_dir, owner: $stack_username, group: $stack_username
    end

    if Vagrant.has_plugin?("vagrant-vbguest")
        config.vbguest.auto_update = false
    end
end
