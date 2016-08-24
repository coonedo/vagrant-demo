Vagrant.configure(2) do |config|
  config.vm.define "vagrant" do |vagrant|
    vagrant.vm.box = "ubuntu/trusty64"
    vagrant.vm.network "private_network", ip: "192.168.0.244"
    vagrant.vm.network :forwarded_port, host: 8080, guest: 80
    vagrant.vm.hostname = "vagrant.demo.com"
    vagrant.vm.provider "virtualbox" do |vb|
      vb.memory = 2048 
      vb.cpus = 2
    end 
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2
  SHELL



end
