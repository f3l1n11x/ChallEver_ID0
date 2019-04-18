# -*- mode: ruby -*-
# vi: set ft=ruby :


VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/7"
  config.ssh.insert_key = false

  config.vm.provision "shell", inline: <<-SHELL
    sudo useradd -p $(openssl passwd -1 password) challenge
    sudo usermod -g wheel challenge
    sudo yum install -y epel-release
    sudo yum update
    sudo yum install -y htop vim
    sudo yum install -y java-1.8.0-openjdk
    #sudo yum install -y nginx
    #systemctl start nginx
    #systemctl enable nginx

  SHELL

  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    #v.linked_clone = true
  end

  # ELK server.
  config.vm.define "logs" do |logs|
    logs.vm.hostname = "logs" 
    logs.vm.network :private_network, ip: "192.168.9.90"

    config.vm.provider :virtualbox do |v|
      v.name = "cent7Logs"
      v.linked_clone = true
    end    
   
    #logs.vm.provision :ansible do |ansible|
    #  ansible.playbook = "provisioning/elk/playbook.yml"
    #  ansible.inventory_path = "provisioning/elk/inventory"
    #  ansible.become = true
    #end
  end

  ## Web server.
  #config.vm.define "webs" do |webs|
  #  webs.vm.hostname = "webs" 
  #  webs.vm.network :private_network, ip: "192.168.9.91"

  #  config.vm.provider :virtualbox do |v|
  #    v.name = "cent7webs"
  #    v.linked_clone = true
  #  end      

  #  webs.vm.provision :ansible do |ansible|
  #    ansible.compatibility_mode = "2.0"
  #    ansible.playbook = "provisioning/web/playbook.yml"
  #    ansible.inventory_path = "provisioning/web/inventory"
  #    ansible.become = true
  #  end
  #end

end

VAGRANT_COMMAND = ARGV[0]



