# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "fedora/33-cloud-base"
    # if you need bigger primary disk
    # config.vm.disk :disk, size: "40GB", primary: true
    # for podman to have container storage
    config.vm.disk :disk, size: "80GB", name: "varlib_containers"

    config.vm.box_check_update = true
    config.vm.network "private_network", ip: "192.168.33.10"
    
    # some common port forwards
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 3306, host: 3306
    config.vm.network "forwarded_port", guest: 5432, host: 5432

    config.vm.provider :virtualbox do |vb|
       vb.name = "podman-machine"
       vb.cpus = 4
       vb.memory = 12288
    end

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      # ansible.verbose  = true
    end

    if Vagrant.has_plugin?("vagrant-vb-gues")
      config.vbguest.auto_update = true
      config.vbguest.no_remote = true
    end
end
