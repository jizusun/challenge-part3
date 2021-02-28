# Single box with VirtualBox provider and Puppet provisioning.

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.provider :virtualbox do |vb|
      vb.customize [
      "modifyvm", :id,
      "--cpuexecutioncap", "50",
      "--memory", "256",
      ]
  end

  config.vm.define "server" do |server|
    server.vm.hostname= "server"
    server.vm.network :private_network, ip: "192.168.0.42"
    server.vm.network :private_network, ip: "10.0.0.2"
    server.vm.network "forwarded_port", guest: 80, host: 8080
    # use the ansible example
    server.vm.provision :ansible do |ansible|
        ansible.playbook = "ansible/site.yml"
    end
  end

  config.vm.define "client" do |client|
    client.vm.hostname= "client"
    client.vm.network :private_network, ip: "192.168.0.43"
    client.vm.network :private_network, ip: "10.0.0.3"
    client.vm.provision "shell", inline: "ping -c 1 192.168.0.42 & ping -c 1 10.0.0.2"
  end

end
