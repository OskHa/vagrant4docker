# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"


docker_hosts = [

]

shared_folder = "./"
config_cpus = 2
config_memory = 4096
config_ip = "172.16.11.10"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "boxcutter/ubuntu1604"
  config.ssh.insert_key = false

  # Virtualbox provider
  # config.vm.provider :virtualbox do |v|
  #   v.name = "docker"
  #
  #   v.customize [
  #     "modifyvm", :id,
  #     "--memory", config_memory,
  #     "--cpus", config_cpus,
  #     "--paravirtprovider", "kvm", # for linux guest
  #     "--cableconnected1", "on",
  #     "--natdnshostresolver1", "on",
  #     "--ioapic", "on"
  #   ]
  #
  # end



  # SSH Agent Forwarding
  #
  # Enable agent forwarding on vagrant ssh commands. This allows you to use ssh keys
  # on your host machine inside the guest. See the manual for `ssh-add`.
  config.ssh.forward_agent = true

  # Parallels provider
  # http://parallels.github.io/vagrant-parallels/docs/configuration.html
  config.vm.provider "parallels" do |prl|
    prl.name = "docker"
    prl.linked_clone = true
    prl.update_guest_tools = true
    prl.name = "docker"
    prl.memory = config_memory
    prl.cpus = config_cpus
  end

  config.vm.hostname = "docker"

  # Set a local private network IP address.
  # See http://en.wikipedia.org/wiki/Private_network for explanation
  # You can use the following IP ranges:
  #   10.0.0.1    - 10.255.255.254
  #   172.16.0.1  - 172.31.255.254
  #   192.168.0.1 - 192.168.255.254

  config.vm.network :private_network, ip: config_ip

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :docker do |docker|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/env/vagrant"
    ansible.sudo = true
  end

  # Use NFS for the shared folder (VirtualBox)
  config.vm.synced_folder shared_folder,
    "/vagrant",
    id: "core"
  #   :nfs => true,
  #   :mount_options => ['nolock,vers=3,udp,noatime,actimeo=2']

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = false
  end

  if Vagrant.has_plugin?("vagrant-hostsupdater")
    config.hostsupdater.aliases = docker_hosts
    config.hostsupdater.remove_on_suspend = true
  end

end
