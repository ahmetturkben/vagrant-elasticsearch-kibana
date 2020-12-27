# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  
    
   config.vm.define "ubuntu-vm2" do |vm2|
	vm2.vm.box_version = "1.0.0"
	vm2.ssh.insert_key = false  
	vm2.vm.hostname = "ubuntu-vm2"
	vm2.vm.box = "gsengun/ubuntu-bare-box-1804"
	vm2.vm.network 'private_network', ip: '192.168.33.20'
	vm2.vm.provider "virtualbox" do |vb|
		vb.name = "ubuntu-vm2"
		vb.gui = false
		vb.memory = "1024"
	end
	vm2.vm.synced_folder ".", "/vagrant", disabled: false  #vagrant fileın bulunduğu yer, vagrant file olarak linux da maple.
	# vm2.vm.synced_folder "./phpScript", "/vagrant/phpScript", disabled: false
	vm2.vm.provision "shell", inline: "cat /vagrant/ansible/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys"
	vm2.vm.provision "shell", inline: "cp /vagrant/ansible/id_rsa /tmp/id_rsa", privileged: false
    vm2.vm.provision "shell", inline: "chmod 600 /tmp/id_rsa", privileged: false
	vm2.vm.provision "shell", inline: "mkdir -p /etc/ansible", privileged: true
    vm2.vm.provision "shell", inline: "cp /vagrant/nginx/inventories/ansible.cfg /etc/ansible/ansible.cfg", privileged: true, run: "always"
	
	 # vm2.vm.provision "shell", inline: <<-SHELL
		 # echo "Hello from the Ubuntu VM2"
	 # SHELL
  end
  
    config.vm.define "ubuntu-vm" do |vm1|
  	vm1.vm.box_version = "1.0.0"
	vm1.ssh.insert_key = false 
	vm1.vm.hostname = "ubuntu-vm"
	vm1.vm.box = "gsengun/ubuntu-bare-box-1804"
	vm1.vm.network 'private_network', ip: '192.168.33.10'
	vm1.vm.provider "virtualbox" do |vb|
		vb.name = "ubuntu-vm"
		vb.gui = false
		vb.memory = "1024"
	end
	vm1.vm.synced_folder ".", "/vagrant", disabled: false
	vm1.vm.provision "shell", inline: "cat /vagrant/ansible/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys"
	vm1.vm.provision "shell", inline: "cp /vagrant/ansible/id_rsa /tmp/id_rsa", privileged: false
    vm1.vm.provision "shell", inline: "chmod 600 /tmp/id_rsa", privileged: false
	vm1.vm.provision "shell", inline: "mkdir -p /etc/ansible", privileged: true
    vm1.vm.provision "shell", inline: "cp /vagrant/nginx/inventories/ansible.cfg /etc/ansible/ansible.cfg", privileged: true, run: "always"	
	 
	 # vm1.vm.provision "shell", inline: <<-SHELL
		 # echo "Hello from the Ubuntu VM"
	 # SHELL
	 vm1.vm.provision "ansible_local" do |ansible|
          ansible.limit = "all"
          ansible.playbook = "/vagrant/nginx/playbooks/ping-playbook.yml"
          ansible.inventory_path = "/vagrant/nginx/inventories/inventory"
          ansible.install_mode = "pip"
          ansible.version = "2.9.10"
        end
  end
  
end
