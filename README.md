# genesis-playbook
This repository forms the beginning of an experimental system - GetGlass.io.

It is meant to automatically install and configure Ansible AWX on a "genesis" host.

In the future an "mcm" role will be added so the Genesis host can be used to securely bootstrap AWX on the MCM instead.

## Requirements
Should work on Ubuntu 18.04, Ubuntu 20.04, CentOS 7, and CentOS 8. Currently only tested on CentOS 8.

You will need Git and Ansible installed.

## Getting Started
* Clone this repository somewhere handy, and cd into it

```
git clone https://github.com/getglass/genesis-playbook.git
cd genesis-playbook
```

* Copy the Genesis variables into place, using the example file. Change them as appropriate.

```
cp .genesis-vars.yml.example ~/.genesis_vars.yml
nano ~/.genesis_vars.yml
```

* Generate an SSH key if you don't already have one

`ssh-keygen`

* Authorize your key to login to your genesis host (which should be localhost).

`ssh-copy-id localhost`

* Perform an Ansible run. If your user does not have passwordless sudo, add --ask-become-pass.

`ansible-playbook site.yml`

## Legal notices
The AWX Project is a trademark of Red Hat, Inc., used with permission.

## Author information
This playbook uses examples and code from https://github.com/geerlingguy/ansible-role-awx which was written by Jeff Geerling.

## Bugs and TODOs
* Needs more testing.
