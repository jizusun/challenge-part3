# Single box with VirtualBox provider and Puppet provisioning.

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "192.168.0.42"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provider :virtualbox do |vb|
    vb.customize [
      "modifyvm", :id,
      "--cpuexecutioncap", "50",
      "--memory", "256",
    ]
  end

  # use the puppet example
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "puppet/manifests"
  #   puppet.manifest_file = "site.pp"
  #   puppet.module_path = "puppet/modules"
  # end

  # use the chef example
  # config.vm.provision :chef do |chef|
  #   chef.cookbooks_path = "chef"
  #   chef.add_recipe 'challenge::default'
  # end

#   use the ansible example
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible/site.yml"
  end
end
