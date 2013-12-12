# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	teamcity_version = "8.0.5"

	config.vm.box = "precise64"
	config.vm.box_url = "http://files.vagrantup.com/precise64.box"
	
	config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", 2048,  "--cpus", "1"]
  	end

	config.vm.network :public_network, guest: 8111, host: 9000
	config.vm.provision :shell, inline: "sudo apt-get update -y"
	config.vm.provision :shell, inline: "sudo apt-get install openjdk-7-jre-headless -y"
	config.vm.provision :shell, inline: "wget http://download.jetbrains.com/teamcity/TeamCity-#{teamcity_version}.tar.gz"
	config.vm.provision :shell, inline: "tar -xvzf TeamCity-#{teamcity_version}.tar.gz"
	config.vm.provision :shell, inline: "export TEAMCITY_DATA_PATH=\"/var/TeamCity/.BuildServer\""
	config.vm.provision :shell, inline: "sudo mkdir -p /home/vagrant/TeamCity/logs"
	config.vm.provision :shell, inline: "sudo chown vagrant:vagrant /home/vagrant/TeamCity/ -R"
	config.vm.provision :shell, inline: "/home/vagrant/TeamCity/bin/teamcity-server.sh start"
	config.vm.provision :shell, inline: "cd /home/vagrant/TeamCity/buildAgent/bin/"
	config.vm.provision :shell, inline: "sudo ./install.sh http://localhost:8111"
end
