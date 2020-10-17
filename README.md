# genesis-playbook
This repository forms the beginning of an experimental system - GetGlass.io.

It is intended to automatically install all of the dependencies for running an Ansible AWX installation, and assist in creating an instance.

The "genesis" host is the one that runs this playbook, and the "mcm" host is the one that will ultimately run an instance of AWX.

## Requirements
Currently this has only been tested on Ubuntu 18.04, but should work on any Ubuntu LTS or mainline Debian release.

Currently this repo only supports building and running the "mcm" on the genesis host.

You will need a recent version of Ansible (2.9 or greater) on the genesis host.

## Getting Started
* Clone this repository somewhere handy

`git clone https://github.com/getglass/genesis-playbook.git`

* Generate an SSH key if you don't already have one

`ssh-keygen`

* Copy your key to user "root".

`ssh-copy-id root@localhost`

* Perform an Ansible run. If your user does not have passwordless sudo, add --ask-become-pass.

`ansible-playbook site.yml -i inventory`

## Legal notices
The AWX Project is a trademark of Red Hat, Inc., used with permission.
