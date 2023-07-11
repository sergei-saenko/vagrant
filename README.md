# VAGRANT
One-command virtual environment boot up

## TO-DO
Complete cluster.yml.<br>
Need to be done following:
- complete mariadb part
- complete cluster creation part

## Tested environment
OS Versions: MacOSX (Monterey 12.6, Ventura 13.1/13.4.1)

### Provider
VirtualBox 7.0.6 r155176

### Vagrant
Vagrant version: 2.3.7 <br>
Vagrant plugins:
  - vagrant-vbguest (0.21.0)
  - vagrant-hostmanager (1.8.9) <br> 
  
Vagrant Boxes:
 + centos/7         (virtualbox, 2004.01)
 + generic/centos6 (virtualbox, 4.1.12)
 + generic/centos9s (virtualbox, 4.1.14)
 + rockylinux/8     (virtualbox, 5.0.0) 
 + rockylinux/9     (virtualbox, 1.0.0) <br>



### User ssh config (add following strings to .ssh/config file in your home dir):
Host * <br>
	StrictHostKeyChecking no





