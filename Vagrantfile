# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box     = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "2048", "--ioapic", "on"]
  end

  config.vm.synced_folder ".", "/vagrant"

  # install docker
  config.vm.provision "shell", inline: <<-SCRIPT
    if [[ ! `which docker > /dev/null 2>&1` ]]; then
      sudo apt-get -y purge docker-engine
      bash <(curl -fsSL https://get.docker.com/)
      # clean up packages that aren't needed
      apt-get -y autoremove
      # add the vagrant user to the docker group
      usermod -aG docker vagrant
    fi
  SCRIPT

  # start docker
  config.vm.provision "shell", inline: <<-SCRIPT
    if [[ ! `service docker status | grep "start/running"` ]]; then
      # start the docker daemon
      service docker start
    fi
  SCRIPT

  # wait for docker to be running
  config.vm.provision "shell", inline: <<-SCRIPT
    echo "Waiting for docker sock file"
    while [ ! -S /var/run/docker.sock ]; do
      sleep 1
    done
  SCRIPT

  # build the docker image
  config.vm.provision "shell", inline: <<-SCRIPT
    echo "Building docker image..."
    cd /vagrant
    docker build -t nanobox/unfs:0.9 --no-cache=true 0.9
    docker tag -f nanobox/unfs:0.9 nanobox/unfs:0.9
  SCRIPT

end
