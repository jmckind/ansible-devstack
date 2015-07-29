# ansible-devstack

Ansible roles and playbooks to provision a DevStack environment.

## Installation

The only real requirement is that you have Ansible installed. A sample Vagrant configuration file has been provided to run in a local VM using VirtualBox.

Open a command prompt and navigate to the project directory

    $ cd PROJECT_DIR

Create the instance using Vagrant and VirtualBox

    $ vagrant up

The ```hosts``` file in the project directory can be updated to point to a cloud instance as an alternative to running in a local VM.

Once an instance is up, run the provisioning playbook. This will install DevStack in the instance. This process can take a long time to complete.

    $ ansible-playbook provision.yml

When the playbook has finished, horizon should be available at [localhost:8800](http://localhost:8800).
