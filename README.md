## WordPress VM with LAMP Stack via Ansible on Vagrant

Setup LAMP Stack with RHEL/CentOS or Debian/Ubuntu using Ansible as provisioner on Vagrant

## Requirements
1. Make sure your machine supports Virtualization
2. VirtualBox installed - get it from https://www.virtualbox.org/wiki/Downloads
3. Vagrant installed - get it from http://www.vagrantup.com/downloads.html


## Getting started
TL;DR
1. Clone this repo to your machine
2. `cd` into this repo and run `vagrant up`

To start using wordpress-vm, do the following:
1. Clone this repo to a preferred directory in your machine
2. `cd` into this repo and update `config.yml` according to your preferences
3. Run `vagrant up`

## Document Root
The folder `html` is where you should place your PHP project. It is mapped to `/var/www/vagrant/html` directory of the VM and is being used by a VirtualHost with a servername `local.dev`.

## Hosts Resolution
In order for your project to be accessible, you need to edit your hosts file and add the following:
```
10.0.0.10 wordpress.vm
```
The IP should correspong to the `vm_ip` provided on `config.yml` in case you modify it.

### Editing hosts file on Windows
For Windows host machine, you can edit your hosts file by doing the ff:
1. Run cmd as administrator
  * Search for cmd in start menu > right click > run as administrator
2. Once in cmd, enter the ff:
  `notepad drivers\etc\hosts`
3. Add the lines above and save

### Editing hosts file on Linux
For Linux host machine, you can edit your hosts file by doing the ff:
1. Launch terminal
2. Once in terminal, enter the ff:
  `sudo vi /etc/hosts`
3. Add the lines above and save

### Automating edit on hosts file
If you want to automate the editing of your hosts file, install the `vagrant-hostsupdater` plugin by running
```
vagrant plugin install vagrant-hostsupdater
```

Once you've updated your hosts file, you can now access your project at http://wordpress.vm

## Ansible Roles
* [ansible-role-repo-epel](https://github.com/geerlingguy/ansible-role-repo-epel) - Installs [EPEL](https://fedoraproject.org/wiki/EPEL) repo
* [ansible-role-mysql](https://github.com/geerlingguy/ansible-role-mysql) - Installs MySQL database server
* [ansible-role-apache](https://github.com/geerlingguy/ansible-role-apache) - Installs Apache server
* [ansible-role-php](https://github.com/geerlingguy/ansible-role-php) - Installs PHP and some of its common modules
* [ansible-role-ppa-ondrej](https://github.com/iambryancs/ansible-role-ppa-ondrej) - Installs [ondrej/php](https://launchpad.net/~ondrej/+archive/ubuntu/php) ppa for Debian/Ubuntu
* [ansible-role-repo-webtatic](https://github.com/iambryancs/ansible-role-repo-webtatic) - Installs the [Webtatic repository](https://webtatic.com/) on RHEL/CentOS
* config-repos - Install repos based on distribution
* [sbaerlocher.wp-cli](https://github.com/sbaerlocher/ansible.wp-cli) - Install [wp-cli](http://wp-cli.org/)
* wordpress - Configure and Install WordPress core and plugins

## License
MIT
