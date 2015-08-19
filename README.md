# Ansible OpenStack Development

Ansible roles and playbooks to provision an OpenStack development environment.


## Installation

The only real requirement is that you have Ansible installed. A sample Vagrant configuration file has been provided to run in a local VM using VirtualBox.

Open a command prompt and navigate to the project directory

    $ cd PROJECT_DIR

Create the instance using Vagrant and VirtualBox

    $ vagrant up

The ```hosts``` file in the project directory can be updated to point to a cloud instance as an alternative to running in a local VM.

Once an instance is up, run the provisioning playbook. This will install the basic dependencies for DevStack in the instance.

    $ ansible-playbook provision.yml

The ```stack.sh``` script will not be run by default, as the process can take a long time to complete. If you would like to have the playbook run it for you, change the ```devstack_run_stack_sh``` variable to "yes" in the devstack role defaults.


## Playbooks

The following playbooks are located in the root project directory and are provided to provision and deploy various aspects of an OpenStack development environment.

#### provision.yml

The provision playbook will setup a base environment for OpenStack development.

#### devstack.yml

The devstack playbook will setup and install DevStack on the instance.

#### devstack.yml

The documentation playbook will setup and install the OpenStack documentation repositories.

#### raxcloud.yml

The raxcloud playbook will provision one or more instances on the Rackspace Public Cloud.
