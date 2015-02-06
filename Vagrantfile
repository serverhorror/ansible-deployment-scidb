# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.ssh.insert_key = false

  if Vagrant.has_plugin?("landrush")
    config.landrush.enabled = true
  end

  (1..3).each do |i|
    config.vm.define "scidb-worker-0#{i}" do |node|
      node.vm.box = "chef/centos-6.5"
      node.vm.host_name = "scidb-0#{i}.vagrant.dev"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end # node.vm.provider
    end # config.vm.define
  end # (1..3)

  config.vm.define "scidb-coordinator" do |node|
    node.vm.box = "chef/centos-6.5"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end # config.vm.provision
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      # ansible.raw_arguments = ["--check"]
      # ansible.raw_arguments = ["--check", "--diff"]
      # ansible.extra_vars = { ansible_ssh_user: "vagrant"}
      ansible.limit = "all"
    end # node.vm.provision
  end # config.vm.define

end # Vagrant.configure
