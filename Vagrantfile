DOCKER_IP   = ENV['DOCKER_IP']   || '192.168.11.100'
DOCKER_PORT = ENV['DOCKER_PORT'] || 4243

Vagrant.configure("2") do |config|
  config.vm.box     = 'precise64'
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'
  config.vm.network :private_network, ip: DOCKER_IP
  config.vm.provision :docker do |d|
    d.pull_images 'base'
  end

  config.vm.provision :shell, inline: <<-SHELL
    sudo sed -i -e 's/DOCKER_OPTS=/DOCKER_OPTS=\"-H #{DOCKER_IP}:#{DOCKER_PORT}\"/g' /etc/init/docker.conf
    sudo service docker restart
  SHELL
end
