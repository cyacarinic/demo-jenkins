# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'pathname'

PROJECT_DIR = Pathname.new(File.expand_path(File.dirname(__FILE__)))
MEMSIZE = "4096"
NUMCPUS = "2"

Vagrant.configure(2) do |config|
    config.vm.box = "centos/7"

    config.vm.network "forwarded_port", guest: 80, host: 80
    config.vm.network "private_network", ip: "192.168.33.10"

    config.vm.synced_folder ENV['DIR'] || PROJECT_DIR, "/usr/local/opt", :nfs => { :mount_options => ["dmode=777","fmode=777"], :owner => "vagrant", :group => "vagrant" }

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", MEMSIZE]
        vb.customize ["modifyvm", :id, "--cpus", NUMCPUS]
    end

    config.vm.provision :ansible do |ansible|
        ansible.playbook = "provisioning/playbook.yml"
    end
end