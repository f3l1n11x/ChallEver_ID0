# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    #override.vm.hostname = hostname
    #v.name = "CentOS"
    v.linked_clone = true   
  end

  # ELK server.|
  config.vm.define "logs" do |logs|
    #logs.vm.name = "CentOS01"
    logs.vm.hostname = "logs"
    logs.vm.network :private_network, ip: "192.168.9.90"

    logs.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/elk/playbook.yml"
      ansible.inventory_path = "provisioning/elk/inventory"
      ansible.become = true
    end
  end


  # Web server.
  config.vm.define "webs" do |webs|
    #webs.vm.name = "CentOS02"
    webs.vm.hostname = "webs"
    webs.vm.network :private_network, ip: "192.168.9.91"

    webs.vm.provision :ansible do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "provisioning/web/playbook.yml"
      ansible.inventory_path = "provisioning/web/inventory"
      ansible.become = true
    end
  end

end
