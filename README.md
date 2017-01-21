# Vagrant for Docker

Default values, replace them under Vagrantfile to fit your needs:

* IP: 172.16.11.10
* CPU: 2
* RAM: 4096 MB
* Shared folder: `./../` 
* Provider: Parallels `(VirtualBox doenst really make sense, the shared-sync is too slow)` 


## Dependencies
----

* Vagrant `1.8`+ (Use `vagrant -v` to check your version)
* Vitualbox or Parallels
* Ansible (Preferred with pip. `pip install ansible`)

## Install
----

* vagrant plugin install vagrant-hostsupdater
* vagrant plugin install vagrant-hostmanager
* (virtualbox) vagrant plugin install vagrant-parallels
* (parallels) vagrant plugin install vagrant-vbguest
* vagrant up

## Update
* vagrant up --provision
* (or if already running) vagrant provision

## Enter the vm (ssh)
* vagrant ssh

## Usage with parallels

Setup:


Requirements:

* Vagrant v1.8 or higher
* Parallels Desktop 8 for Mac or higher

Note: In Parallels Desktop 11 for Mac, only Pro and Business editions are compatible with this Vagrant provider. Standard edition doesn't have a command line functionality and can not be used with Vagrant.

## Potential Issues

* **vagrant up hangs on: Mounting NFS shared folders"**: The firewall is probably blocking incoming NFS connections to the host. On Ubuntu-based machines, use:  `sudo ufw allow in on vboxnet0`
* **Plugins are not up to date**: Run: `vagrant plugin expunge --reinstall`
