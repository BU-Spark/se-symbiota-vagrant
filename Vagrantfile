# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "generic/ubuntu1804"
  config.vm.define :vagrant_symbiota do |vagrant_host|
    vagrant_host.vm.hostname = "symbiota"
    vagrant_host.vm.provider :libvirt do |domain|
      domain.cpus = 2
      #domain.memory = 4096
      domain.memory = 8192
      domain.nested = true

      vagrant_host.vm.synced_folder "www-html/", "/var/www/html", create: true, type: "nfs", nfs_version: 4

    end
    vagrant_host.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      # vb.gui = true
      # Another bug: https://github.com/chef/bento/issues/682
        vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
      #
      #   # Customize the amount of memory on the VM:
      #   vb.memory = "1024"

      # Create a private network, which allows host-only access to the machine
      # using a specific IP.
      vagrant_host.vm.network "private_network", ip: "192.168.33.10"

      vagrant_host.vm.synced_folder "www-html/", "/var/www/html", create: true
    end

    vagrant_host.vm.provider "vmware_desktop" do |vb|
      vagrant_host.vm.synced_folder "www-html/", "/var/www/html", create: true
    end

    # Define the bootstrap file: A (shell) script that runs after first setup of your box (= provisioning)
    vagrant_host.vm.provision :shell, path: "bootstrap.sh"
    vagrant_host.vm.provision :shell, path: "symbiota.sh"
  end
end
