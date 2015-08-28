# Ansible OpenStack Development

Ansible roles and playbooks to provision OpenStack development environments.


## Overview

The only real requirement is that Ansible is installed. The current platforms supported are Vagrant (with VirtualBox) for local deployments and Rackspace Public Cloud for cloud deployments. However, the playbooks should work with any remote environment with an appropriate Ansible hosts file.


## Usage - Vagrant

A sample Vagrant configuration file has been provided to run in a local VM using VirtualBox.

Open a command prompt and navigate to your local project directory

    $ cd PROJECT_DIR

Create the instance using Vagrant and VirtualBox

    $ vagrant up

Once the instance is up, run the provisioning playbook. This will install the basic dependencies on the instance.

    $ ansible-playbook provision.yml
    $ vagrant reload

When the instance has reloaded, the software can be installed.

To work on the the OpenStack codebase, install DevStack. This can take a while, as all of the OpenStack core components are being installed from source.

    $ ansible-playbook devstack.yml

The OpenStack documentation can be installed as well for working on that.

    $ ansible-playbook documentation.yml


## Usage - Rackspace Cloud

Open a command prompt and navigate to your local project directory

    $ cd PROJECT_DIR

The first step is to configure the credentials that will be used for the Rackspace Cloud account. This information can be found on the account page of the [Rackspace Cloud Control Panel](http://mycloud.rackspace.com/).

Create a file named `all` (no extension) in the `group_vars` directory to hold the credentials.

    # group_vars/all
    ---

    rax_tenant_id: <ACCOUNT_ID>
    rax_username: <USERNAME>
    rax_password: <API_KEY>

Once the credentials are in place, run the playbook to create the cloud servers.

    $ ansible-playbook raxcloud.yml

The playbook will ask a few questions about the lab environment. Any optional parameters will be listed in brackets [].

    Rackspace Cloud Region [IAD]: DFW
    Name for the group of instances (Ex. testing): test
    Number of instances [1]: 1

When the playbook has completed, an inventory and hosts file should be present in the project directory.

    hosts-raxcloud-test
    inventory-raxcloud-test.html

The hosts file must be used when running the other playbooks against the cloud environment.

    $ ansible-playbook -i hosts-raxcloud-test provision.yml
    $ ansible-playbook -i hosts-raxcloud-test devstack.yml
    $ ansible-playbook -i hosts-raxcloud-test documentation.yml

The inventory file can be opened with a browser and used to view information on the nodes in the environment.

* Mac

    ```
    $ open inventory-raxcloud-test.html
    ```

* Linux

    ```
    TODO
    ```


## Playbook Reference

The following playbooks are located in the root project directory and are provided to provision and deploy various aspects of an OpenStack development environment.

#### provision.yml

The provision playbook will setup a base environment for OpenStack development.

#### devstack.yml

The devstack playbook will setup and install DevStack on the instance.

#### documentation.yml

The documentation playbook will setup and install the OpenStack documentation repositories.

#### raxcloud.yml

The raxcloud playbook will provision one or more instances on the Rackspace Public Cloud.
