# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "CentOS-6.4"

  config.vm.define 'postgres-1' do |machine|
    machine.vm.hostname = 'postgres-1'
    machine.vm.network 'private_network', ip: "192.168.77.10"
  end
  config.vm.define 'postgres-2' do |machine|
    machine.vm.hostname = 'postgres-2'
    machine.vm.network 'private_network', ip: "192.168.77.11"
  end
  config.vm.define 'postgres-3' do |machine|
    machine.vm.hostname = 'postgres-3'
    machine.vm.network 'private_network', ip: "192.168.77.12"

    machine.vm.provision :ansible do |ansible|
      ansible.playbook = "postgres.yml"
      ansible.limit = "all"
      ansible.sudo = true
      ansible.groups = {
        "postgres" => ["postgres-1", "postgres-2", "postgres-3"]
      }
    end
  end
end