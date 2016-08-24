vagrant-demo README
==================


Created by: Donal Cooney

Note: 	This demo is a very basic introduction to the topic named above created 
	purely as a tutorial for myself. Absolutely no gaurantees whatsoever 
	wrt these instructions and/or software.



Vagrant is used to create and configure virtual environments. Vagrant
provides a wrapper around VirtualBox, AWS, Docker, VMWare, Hyper-V ....




Vagrant-demo Summary:
--------------------

1.	Run a linux virtual box (ubuntu) on PC (virtualbox)
2. 	Provision the linux box with Apcahe2





Instructions:
-------------

-	START DEMO
- 	Windoze: Create a directory 'vagrant_project'

-	Download vagrant, virtualbox, putty & puttygen


	Download the latest Virtualbox from https://www.virtualbox.org/
	Download the latest Vagrant from https://www.vagrantup.com/
	Download putty and puttygen from
	http://www.chiark.greenend.org.uk/~sgtatham/putty/...



- 	Windoze: From dir 'vagrant_project', clone this repo to get
	the Vagrantfile 

        https://github.com/coonedo/vagrant-demo	



Vagrant.configure(2) do |config|
  config.vm.define "vagrant" do |vagrant|
    vagrant.vm.box = "ubuntu/trusty64"
    vagrant.vm.network "private_network", ip: "192.168.0.244"
    vagrant.vm.network :forwarded_port, host: 8080, guest: 80
    vagrant.vm.hostname = "vagrant.demo.com"
    vagrant.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2
  SHELL

end




- 	Windoze: From dir 'vagrant_project', run the following command: 
	'vagrant up'
	C:\Users\coonedo\docker_project>vagrant up

	wait  ..........






-	We now have:
	A ubuntu linux instance running (virtualised using virtualbox on pc	
	Ipadress 192.168.0.244 assigned
	Port forwarding from 8080 on host to 80 on the linux box (not used)
	Port forwarding automatically set up for SSH (22/2222)
	2Gbytes memory
	apache2 running



-	curl localhost:8080 OR point browser to localhost:8080
	Apache2 is running




-	you can also ssh into the box
	vagrant ssh



C:\Users\coonedo\vagrant_project>vagrant ssh
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.13.0-83-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Wed Aug 24 21:06:59 UTC 2016

  System load:  1.34              Processes:           93
  Usage of /:   3.5% of 39.34GB   Users logged in:     0
  Memory usage: 6%                IP address for eth0: 10.0.2.15
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

New release '16.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


vagrant@vagrant:~$





-       An alternative (better) means to connect is via putty


	Convert the vagrant private key:
	Using puttygen you downloaded from the putty website, convert the 
	OpenSSH private key to a putty-readable key:

	Make sure your vagrant box is running (vagrant up in project folder)
	Type the command vagrant ssh-config to display the ssh configuration. 
	You can find the path to the private key next to IdentityFile
	Open puttygen
	Click on the Load button
	Navigate to the path shown by vagrant ssh-config (next to IdentityFile)
	Select the private_key
	Now click on the ŒÈŒÌSave private keyŒÈŒÌ button and save the file as 
	.ppk file somewhere where you can easily find it


	Use putty to log into your Vagrant machines
	Open putty and configure the following parameters:

	Session:
	Host: 127.0.0.1
	Port: 2222 and up (depends on how many vagrant machines you launch)
	Connection
	Data
	Auto-login username: vagrant
	Connection/SSH
	Auth
	Private key file for auth: Click browse and select your ppk file
	Session
	Save the session to save the parameters you just entered


















