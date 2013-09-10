# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "base-hadoop"

    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "manifests"
        puppet.manifest_file  = "base-hadoop.pp"
        puppet.module_path = "modules"
    end

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
    end

    config.vm.define :backup do |backup_config|
        backup_config.vm.network :private_network, ip: "192.168.1.11"
        backup_config.vm.hostname = "backup"
    end

    config.vm.define :hadoop1 do |hadoop1_config|
        hadoop1_config.vm.network :private_network, ip: "192.168.1.12"
        hadoop1_config.vm.hostname = "hadoop1"
    end

    config.vm.define :hadoop2 do |hadoop2_config|
        hadoop2_config.vm.network :private_network, ip: "192.168.1.13"
        hadoop2_config.vm.hostname = "hadoop2"
    end

    config.vm.define :hadoop3 do |hadoop3_config|
        hadoop3_config.vm.network :private_network, ip: "192.168.1.14"
        hadoop3_config.vm.hostname = "hadoop3"
    end

    config.vm.define :master do |master_config|
        master_config.vm.network :private_network, ip: "192.168.1.10"
        master_config.vm.hostname = "master"
        master_config.vm.network :forwarded_port, guest: 50070, host: 50070
        master_config.vm.network :forwarded_port, guest: 50030, host: 50030
    end
end
