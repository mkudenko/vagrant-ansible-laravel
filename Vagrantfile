# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant LAMP Ansible Laravel
# A Laravel development platform in a box.
# See the readme file (README.md) for more information.

# Find the current vagrant directory.
vagrant_dir = File.expand_path(File.dirname(__FILE__))

# Include config from provision/settings.yml
require 'yaml'
vconfig = YAML::load_file(vagrant_dir + "/provision/settings.yml")

# Configuration
boxipaddress = vconfig['boxipaddress']
boxname = vconfig['boxname']

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Configure virtual machine options.
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = boxname

  config.vm.network :private_network, ip: boxipaddress

  # Set *Vagrant* VM name
  config.vm.define boxname do |boxname|
  end

  # Configure virtual machine setup.
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--cpus", vconfig["cpus"] ||= "1"]
    v.customize ["modifyvm", :id, "--memory", vconfig["memory"] ||= "1024"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  # Set up NFS drive.
  nfs_setting = RUBY_PLATFORM =~ /darwin/ || RUBY_PLATFORM =~ /linux/

  # Setup synced folder for site files
  config.vm.synced_folder "./webroot",
    "/home/vagrant/sites/" + vconfig["webserver_hostname"],
    type: "nfs",
    create: true

  # SSH Set up.
  config.ssh.forward_agent = true

  # Provision vagrant box with Ansible.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = vagrant_dir + "/provision/playbooks/setup.yml"
    ansible.host_key_checking = false
    ansible.extra_vars = {user:"vagrant"}
    if vconfig['ansible_verbosity'] != ''
      ansible.verbose = vconfig['ansible_verbosity']
    end
  end

end
