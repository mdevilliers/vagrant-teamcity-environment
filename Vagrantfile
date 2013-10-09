# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

	teamcity_version = "8.0.3"

	config.vm.box = "precise64"
	config.vm.box_url = "http://files.vagrantup.com/precise64.box"
	
	config.vm.customize ["modifyvm", :id,
                        "--memory", 2048,
                        "--cpus",     "1"]
	
	config.vm.network :bridged, guest: 8111, host: 9000
	config.vm.provision :shell, inline: "sudo apt-get update -y"
	config.vm.provision :shell, inline: "sudo apt-get install openjdk-7-jre-headless -y"
	config.vm.provision :shell, inline: "wget http://download.jetbrains.com/teamcity/TeamCity-#{teamcity_version}.tar.gz"
	config.vm.provision :shell, inline: "tar -xvzf TeamCity-#{teamcity_version}.tar.gz"
	config.vm.provision :shell, inline: "export TEAMCITY_DATA_PATH=\"/var/TeamCity/.BuildServer\""
	config.vm.provision :shell, inline: "sudo mkdir -p /home/vagrant/TeamCity/logs"
	config.vm.provision :shell, inline: "sudo chown vagrant:vagrant /home/vagrant/TeamCity/ -R"
	config.vm.provision :shell, inline: "/home/vagrant/TeamCity/bin/teamcity-server.sh start"
	config.vm.provision :shell, inline: "/home/vagrant/TeamCity/buildAgent/bin/install.sh http://localhost:8111"
end
