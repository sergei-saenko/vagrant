# -*- mode: ruby -*-
# vi: set ft=ruby :

# Tested on
# Vagrant version: "2.3.4"
# OS version: "MacOS Monterey 12.6"
# VirtualBox version: 7.0.6
# VmWare Fusion (macosx): not tested

PRIVATE_NET="192.168.56."
#DOMAIN=".local"

servers =[
	
{
	:hostname => "rocky9",
	:box => "rockylinux/9",
    	:ip => PRIVATE_NET + "10",
    	:ram => 4096,
	:cpunum => 2
  },
{
	:hostname => "rocky8",
	:box => "rockylinux/8",
	#:box => "ubuntu/bionic64",
    	#:hostname => "c1" + DOMAIN,
    	:ip => PRIVATE_NET + "20",
	:ram => 1024,
	:cpunum => 2
  	# :ip_int => "1",
	# :hdd_name => "db2_hdd.vdi",
  	# :hdd_size => "10000"
  }, 
{
	:hostname => "centos7",
	:box => "centos/7",
    	:ip => PRIVATE_NET + "30",
    	:ram => 1024,
	:cpunum => 1
  },	
{
	:hostname => "centos6",
	:box => "generic/centos6",
    	:ip => PRIVATE_NET + "40",
    	:ram => 1024,
	:cpunum => 1
  },
{
	:hostname => "ubuntu16",
	:box => "ubuntu/xenial64",
    	:ip => PRIVATE_NET + "50",
    	:ram => 1024,
	:cpunum => 1
  },
{
	:hostname => "rhel8",
	:box => "generic/rhel8",
    	:ip => PRIVATE_NET + "60",
    	:ram => 1024,
	:cpunum => 1
  },
  {
	:hostname => "acontrol",
	:box => "rockylinux/8",
    :ip => PRIVATE_NET + "80",
	:ram => 1024,
	:cpunum => 2
  }, 
  {
	:hostname => "aclient1",
	:box => "rockylinux/8",
    :ip => PRIVATE_NET + "81",
	:ram => 1024,
	:cpunum => 1
  }, 
  {
	:hostname => "aclient2",
	:box => "rockylinux/8",
    :ip => PRIVATE_NET + "82",
	:ram => 1024,
	:cpunum => 1
  } 
]


Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
		servers.each do |machine|	
			config.vm.define machine[:hostname] do |node|
					node.vm.box = machine[:box]
					node.vm.usable_port_range = (2200..2250)
					node.vm.hostname = machine[:hostname]
					node.vm.network "private_network", ip: machine[:ip]
					# SSH Setup
					# fqdn/ip for connection
					#node.ssh.host = machine[:ip]
					# for ssh-key based access via previosly added key
					#node.ssh.private_key_path = "private_key"
					# SSH login of the user
					# node.ssh.username = "someuser"
					# SSH password
					#node.ssh.password = "vagrant"
					node.vm.provider "virtualbox" do |vb|
							vb.name = machine[:hostname]
							vb.cpus = machine[:cpunum]
							vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
							node.vm.provision :ansible do |ansible|
								ansible.playbook = "provisioning/post.yml"
							end
							# Adding HDD in case if it was specified in servers block (where VMs parameters defined)
							if (!machine[:hdd_name].nil?)
									unless File.exist?(machine[:hdd_name])
											vb.customize ["createhd", "--filename", machine[:hdd_name], "--size", machine[:hdd_size]]
							  end
							vb.customize ["storageattach", :id, "--storagectl", "SATA", "--port", 1, "--device", 0, "--type", "hdd", "--medium", machine[:hdd_name]]
							end
					
			 end
		 end
	 end
	end
