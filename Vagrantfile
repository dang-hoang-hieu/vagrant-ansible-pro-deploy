# -*- mode: ruby -*-
# vi: set ft=ruby :

# ===============================
# Vagrant
# ===============================
VAGRANT_USER = ENV['USER'] || 'anonymous'

Vagrant.configure('2') do |config|
  config.vm.box = "tknerr/managed-server-dummy"
  config.vm.provider :managed do |managed, override|
    managed.server = ENV['IP_SERVER']
    override.ssh.username = ENV['SSH_USER']
    override.ssh.private_key_path = ENV['KEY_PATH']
    ## Provisioning ##
    config.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'provision/playbook.yml'
      ansible.extra_vars = {
        VAGRANT_USER: VAGRANT_USER
      }
    end
    config.vm.synced_folder '.', '/vagrant', disabled: true
  end
end
