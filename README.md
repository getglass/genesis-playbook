# genesis-playbook
This repository forms the beginning of an experimental system - GetGlass.io.

It is intended to automatically install all of the dependencies for running an Ansible AWX installation, and assist in creating an instance.

The "genesis" host is the one that runs this playbook, and the "mcm" host is the one that will ultimately run an instance of AWX.

## Requirements
The Genesis host can run any of the following:
* CentOS 7 (untested) or CentOS 8
* Ubuntu 18.04 (Ubuntu 20.04 should work too but is currently broken)
* Debian 10 (untested)

Currently this repo only supports building and running the "mcm" on the genesis host. One potential approach to solve this is not to include localhost in the mcm inventory group, so that the mcm role only runs if there is a custom mcm defined. Then it would simply deploy Docker on the mcm and inject it into the awx inventory file.

You will need a recent version of Ansible (2.9 or greater) on the genesis host - the playbook will upgrade the genesis host to use the latest stable.

## Getting Started
* Clone this repository somewhere handy, and cd into it

```
git clone https://github.com/getglass/genesis-playbook.git
cd genesis-playbook
```

* Generate an SSH key if you don't already have one

`ssh-keygen`

* Authorize your key to login to your genesis host (which should be localhost).

`ssh-copy-id localhost`

* Perform an Ansible run. If your user does not have passwordless sudo, add --ask-become-pass.

`ansible-playbook site.yml -i inventory`

## Deploying AWX
* Copy .genesis-vars.yml.example to ~/.genesis-vars.yml

`cp .genesis-vars.yml.example ~/.genesis-vars.yml`

* Fill out ~/.genesis-vars.yml with your initial seed data.

This file is INCREDIBLY sensitive. Treat it like the keys to your kingdom, because it *is* the keys to your kingdom.

* Change to the awx directory

`cd ~/awx/installer`

* Run the installer playbook

`ansible-playbook -i inventory install.yml -e @$HOME/.genesis-vars.yml`

## Legal notices
The AWX Project is a trademark of Red Hat, Inc., used with permission.

## Bugs and TODOs
* You must manually add yourself to the Docker user group before attempting to deploy the MCM. Example -

`sudo usermod -aG docker wings`

* On Ubuntu 18.04 the glass-genesis role fails after upgrading Ansible. Re-running the playbook works fine, however.
