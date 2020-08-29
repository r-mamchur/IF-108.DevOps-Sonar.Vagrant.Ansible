# -*- mode: ruby -*-
# vi: set ft=ruby :
num_of_be = 2
num_of_fe = 2

Vagrant.configure("2") do |config| 

   config.vagrant.host = "windows"
   config.vm.box_check_update = true
   config.ssh.insert_key = false

   config.vm.define "sonar" do |sonar|
      sonar.vm.box = "centos/8"
      sonar.vm.hostname = 'sonar'
      sonar.vm.network "private_network", ip: "192.168.56.225"
      sonar.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
      sonar.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/vagrant/insecure_private_key"
      sonar.vm.provision "shell", inline: "chmod 0600 /vagrant/insecure_private_key"
   
      sonar.vm.provision "shell", path: "root_ssh.sh"	
      sonar.vm.provision "ansible_local" do |ansible|
         ansible.playbook = "playbook.yml"
         ansible.limit = "all"
         ansible.verbose = true
         ansible.install = true
      end
   end

end

