# -*- mode: ruby -*-
# vi: set ft=ruby :

$setupscript = <<END
  # Install git, apache and sqlite
  sudo apt-get update
  sudo apt-get install -y git apache2 sqlite sqlite3 libsqlite3-dev
  # Clean up
  sudo apt-get autoremove
  # Install gpg key for RVM
  sudo gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
  # Install lastest stable version of RVM with ruby
  sudo curl -sSL https://get.rvm.io | bash -s stable --ruby
  # Add vagrant user to rvm group
  sudo usermod -a -G rvm vagrant
  source /usr/local/rvm/scripts/rvm
  source /etc/profile.d/rvm.sh
  # Install lastest version of rails
  gem install rails --no-rdoc --no-ri
END

$ipaddress = "192.168.250.100"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

# boxes
  config.vm.define "rails", primary: true do |rails|
    rails.vm.hostname = "r1"
    rails.vm.network :private_network, ip: $ipaddress
    rails.vm.provision :shell, inline: $setupscript
  end

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
   end
end
