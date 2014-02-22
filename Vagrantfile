# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu-docker"
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/ubuntu-12.04.3-amd64-vbox.box"

  (0..1).to_a.each do |index|
    ip= 100 + index
    config.vm.define "drbd-#{index}", primary: true do |v|
      v.vm.network "private_network", ip: "192.168.69.#{ip}"
      v.vm.hostname = "drbd-#{index}"
      v.persistent_storage.enabled = true
      v.persistent_storage.location = "./tmp/source-#{index}.vdi"
      v.persistent_storage.size = 5000
      v.persistent_storage.filesystem = 'ext4'
      v.persistent_storage.mountpoint = '/var/lib/mysql'
      v.persistent_storage.volgroupname = 'myvolgroup'
      v.persistent_storage.diskdevice = "/dev/sdb"
      v.persistent_storage.mount = false
      v.persistent_storage.use_lvm = false
      v.vm.provision "shell" do |sh|
        sh.path = "bin/provision"
      end
    end
  end

end
