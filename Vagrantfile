# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

file_to_disk1 = 'data/g1disk2.vdi'
file_to_disk2 = 'data/g2disk2.vdi'
file_to_disk0 = 'data/g0disk2.vdi'
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.define "glus1" do |g1|
    g1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus1"
      unless File.exist?(file_to_disk1)
        vb.customize ['createhd', '--filename', file_to_disk1, '--size', 5 * 1024]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk1]
    end
  end
  config.vm.define "glus2" do |g2|
    g2.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus2"
      unless File.exist?(file_to_disk2)
        vb.customize ['createhd', '--filename', file_to_disk2, '--size', 5 * 1024]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk2]
    end
  end
  config.vm.define "glus0" do |g0|
    g0.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus0"
      unless File.exist?(file_to_disk0)
        vb.customize ['createhd', '--filename', file_to_disk0, '--size', 5 * 1024]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk0]
    end
  end
end
