# -*- mode: ruby -*-
# vi: set ft=ruby :

# ===============================
# Vagrant
# ===============================

Vagrant.configure('2') do |config|
  config.vm.define :jenkins do |jenkins|
    jenkins.vm.box = "tknerr/managed-server-dummy"
    jenkins.vm.provider :managed do |managed, override|
      managed.server = ENV['JENKINS_IP_SERVER']
      override.ssh.username = ENV['JENKINS_SSH_USER']
      override.ssh.private_key_path = ENV['JENKINS_KEY_PATH']
      ## Provisioning ##
      jenkins.vm.provision 'ansible' do |ansible|
        ansible.playbook = 'provision/playbook-jenkins.yml'
        ansible.extra_vars = {
          VAGRANT_USER: "jenkins"
        }
      end
      jenkins.vm.synced_folder '.', '/vagrant', disabled: true
    end
  end

  config.vm.define :web do |web|
    web.vm.box = "tknerr/managed-server-dummy"
    web.vm.provider :managed do |managed, override|
      managed.server = ENV['WEB_IP_SERVER']
      override.ssh.username = ENV['WEB_SSH_USER']
      override.ssh.private_key_path = ENV['WEB_KEY_PATH']
      override.ssh.forward_agent = true
      ## Provisioning ##
      web.vm.provision 'ansible' do |ansible|
        ansible.playbook = 'provision/playbook-web.yml'
        ansible.extra_vars = {
          VAGRANT_USER: "deploy",
          mysql_user: ENV['WEB_MYSQL_USER'],
          mysql_passwd: ENV['WEB_MYSQL_PASSWD']
        }
      end
      web.vm.synced_folder '.', '/vagrant', disabled: true
    end
  end
end
