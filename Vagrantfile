# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'


vagrant_dir = File.dirname(File.expand_path(__FILE__))

require 'yaml'

conf = YAML.load_file("#{vagrant_dir}/config.yml")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = conf['vm_box']
  config.vm.network :private_network, ip: conf['vm_ip']
  config.vm.hostname = conf["vm_hostname"]

  config.vm.synced_folder '.', conf["guest_vagrant_dir"], mount_options: ['dmode=0775', 'fmode=0664']

  # Set name
  config.vm.define conf['vm_name']

  config.vm.provider :virtualbox do |vb|
    vb.name = conf["vm_hostname"]
  end

  if Vagrant.has_plugin?('vagrant-hostsupdater')
    config.hostsupdater.aliases = %W{www.#{conf["vm_hostname"]}}
  end

  config.vm.provision :ansible_local do |ansible|
    ansible.provisioning_path = conf["guest_vagrant_dir"]
    ansible.playbook       = 'provisioning/playbook.yml'
    ansible.verbose        = true
    ansible.install        = true
    ansible.limit          = 'all'
    ansible.galaxy_role_file = 'requirements.yml'
    ansible.inventory_path = 'provisioning/inventory'
    ansible.extra_vars     = 'config.yml'
  end
end
