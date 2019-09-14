# -*- mode: ruby -*-
# vi: set ft=ruby :

# Define the cluster
nodes = [
  { :hostname => 'xwiki1', :ip => '10.0.0.49', :extport => '80', :mem => '3072', :cpus => '2'}
]

Vagrant.configure("2") do |config|
    # # install vagrant-cachier upfront with $ vagrant plugin install vagrant-cachier
    # if Vagrant.has_plugin?("vagrant-cachier")
    #   config.cache.scope = :box
    #   config.cache.synced_folder_opts = { type: :nfs, mount_options: ['rw', 'vers=3', 'tcp', 'nolock'] }
    # end

    # install vagrant-hostmanager upfront with vagrant plugin install vagrant-hostmanager
  config.hostmanager.enabled = false
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true
  config.hostmanager.ignore_private_ip = false

  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|

      node_config.vm.hostname = node[:hostname]
      node_config.vm.network :private_network, ip: node[:ip]

      node_config.vm.box = "ubuntu/bionic64"
      node_config.disksize.size = '16GB'

      node_config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
      #node_config.vm.network "forwarded_port", guest: 8080, host: node[:extport]
      node_config.vm.provision :hostmanager

      node_config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", node[:mem], "--cpus", node[:cpus]]
      end

      config.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "xwiki_runbook.yml"
      end

    end
  end

end
