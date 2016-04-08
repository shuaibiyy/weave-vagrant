# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT

# Install kernel extra's to enable docker aufs support
sudo apt-get -y install linux-image-extra-$(uname -r)

# Add Docker PPA and install latest version
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
sudo sh -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
sudo apt-get update
sudo apt-get install lxc-docker -y

# Install Weave
sudo curl -L git.io/weave -o /usr/local/bin/weave
sudo chmod a+x /usr/local/bin/weave

# For weave environment settings and cutting down on sudo.
echo 'eval $(sudo weave env)' >> ~/.bashrc
echo "alias weave='sudo weave'" >> ~/.bashrc
echo "alias docker='sudo docker'" >> ~/.bashrc

sudo weave launch
eval $(sudo weave env)

SCRIPT

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 8080, host: 8181
    config.vm.network "forwarded_port", guest: 4040, host: 4040

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: $script, privileged: false

end
