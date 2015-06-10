# -*- mode: ruby -*-
# vi: set ft=ruby :

$provision_script = <<SCRIPT
  apt-get update
  apt-get install -y apt-cacher-ng
  cp /vagrant/conf/acng.conf /etc/apt-cacher-ng/
  /etc/init.d/apt-cacher-ng restart
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "chef/debian-7.8"

  config.vm.network "private_network", ip: "192.168.33.254"

  config.vm.provision "shell", inline: $provision_script
end
