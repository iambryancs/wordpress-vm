## WordPress VM with LAMP Stack via Ansible on Vagrant

[![Build Status](https://travis-ci.org/iambryancs/wordpress-vm.svg?branch=master)](https://travis-ci.org/iambryancs/wordpress-vm)

Setup WordPress VM with LAMP Stack on RHEL/CentOS or Debian/Ubuntu using Ansible as provisioner on Vagrant

## Requirements
1. Make sure your machine supports Virtualization
2. VirtualBox installed - get it from https://www.virtualbox.org/wiki/Downloads
3. Vagrant installed - get it from http://www.vagrantup.com/downloads.html


## Getting started
TL;DR
1. Clone this repo to your machine
2. `cd` into this repo and run `vagrant up`
3. Update hosts file and add `10.0.0.10 wordpress.vm`
4. Access project at `http://wordpress.vm`

To start using wordpress-vm, do the following:
1. Clone this repo to a preferred directory in your machine
2. `cd` into this repo and update `config.yml` according to your preferences

   A few variables you can play in `config.yml`
   - `vm_box` - You can try any distro verions under RHEL or Debian (e.g. `ubuntu/trusty64`, `geerlingguy/centos7`)
   - `vm_ip` - Change to any private IP you prefer or leave as is
   - `vm_name` - Set your VM's name
   - `vm_hostname` - Set the hostname of your VM. This is also used as WordPress' base url.
   - `wp_project_dir_name` - Directory name where wordpress is installed
   - `wp_db_name` - Database name used by WordPress and provisioned by `geerlingguy.mysql` ansible role.
   - `wp_db_user` - Database user used by WordPress and provisioned by `geerlingguy.mysql` ansible role.
   - `wp_db_pass` - Database password used by WordPress and provisioned by `geerlingguy.mysql` ansible role.
3. Run `vagrant up`
4. Update your hosts file

   In order for your project to be accessible, you need to edit your hosts file and add the following:
   ```
   10.0.0.10 wordpress.vm
   ```
   The IP should correspond to the `vm_ip` provided on `config.yml` in case you modify it.

   - Editing hosts file on Windows
   
     For Windows host machine, you can edit your hosts file by doing the ff:
     1. Run cmd as administrator > search for cmd in start menu > right click > run as administrator
     2. Once in cmd, type and enter `notepad drivers\etc\hosts`
     3. Add `10.0.0.10 wordpress.vm` and save

   - Editing hosts file on Linux
   
     For Linux host machine, you can edit your hosts file by doing the ff:
     1. Launch terminal
     2. Once in terminal, type and enter `sudo vi /etc/hosts`
     3. Add `10.0.0.10 wordpress.vm` and save

   - Automating edit on hosts file
   
     If you want to automate the editing of your hosts file, install the `vagrant-hostsupdater` plugin by running
     ```
     vagrant plugin install vagrant-hostsupdater
     ```
     You will need to run your CMD as admin on Windows when doing this.
     
5. Once you've updated your hosts file, you can now access your project at http://wordpress.vm

## WordPress Admin
The default `username` and `password` for `wp-admin` is `admin` for both.

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

## To do
1. Make VM more customizable through config (e.g. cpu, memory)
2. Add test suite for Travis-CI

## License
MIT
