# VAGRANT
One-command virtual environment boot up. <br>
You should have a ssh-key private and public with following naming:
- id_rsa_vagrant
- id_rsa_vagrant.pub
There should be located in your user ~/.ssh directory.

## Tested environment
OS Versions: MacOSX (Monterey 12.6, Ventura 13.1/13.4.1)

### Provider
VirtualBox 7.0.12 r159484

### Vagrant
Vagrant version: 2.4.0 <br>
Vagrant plugins:
  - vagrant-vbguest (0.21.0)
  - vagrant-hostmanager (1.8.9) <br> 
  
Vagrant Boxes:
 + centos/7         (virtualbox, 2004.01)
 + generic/centos6  (virtualbox, 4.3.4)
 + generic/centos9s (virtualbox, 4.1.14)
 + rockylinux/8     (virtualbox, 5.0.0) 
 + rockylinux/9     (virtualbox, 2.0.0) 
 + generic/rhel8    (virtualbox, 4.2.14) 
 + ubuntu/xenial64  (virtualbox, 20211001.0.0) <br>



### User ssh config (add following strings to .ssh/config file in your home dir):
Host * <br>
	StrictHostKeyChecking no

### TO-DO:
Complete cluster.yml.<br>
Need to be done following:
- complete mariadb part
- complete cluster creation part

### Not solved issues
1. generic/centos6: ansible provision doesn work, error is below:<br>
TASK [Gathering Facts] *********************************************************
fatal: [vag-centos6]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Unable to negotiate with 127.0.0.1 port 2204: no matching host key type found. Their offer: ssh-rsa", "unreachable": true} <br>

2. ubuntu/xenial64: ansible is not able to hadnle selinux on ubuntu 16, here is error:<br>
TASK [INITIAL SETUP - Selinux is disabled] *************************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: ImportError: No module named 'selinux'
fatal: [vag-ubuntu16]: FAILED! => {"changed": false, "msg": "Failed to import the required Python library (libselinux-python) on vag-ubuntu16's Python /usr/bin/python3. Please read the module documentation and install it in the appropriate location. If the required library is installed, but Ansible is using the wrong Python interpreter, please consult the documentation on ansible_python_interpreter"}<br>






