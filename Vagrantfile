# -*- mode: ruby -*-
# Copyright (C) 2017 Luis Perez luis.luimarin@gmail.com
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program.  If not, see <http://www.gnu.org/licenses/>.
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

file_to_disk1 = 'data/g1disk2.vdi'
file_to_disk2 = 'data/g2disk2.vdi'
file_to_disk0 = 'data/g0disk2.vdi'
size_disk = 7 * 1024
gluster_version = 40
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
#    ansible.limit = "all"
    ansible.extra_vars = {
      gluster_version: gluster_version
    }
  end
  config.vm.define "glus1" do |g1|
    g1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus1"
      unless File.exist?(file_to_disk1)
        vb.customize ['createhd', '--filename', file_to_disk1, '--size', size_disk]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk1]
    end
    g1.vm.network "private_network", ip: "10.10.2.11"
    g1.vm.hostname = "glus1.corp.itm.gt"
  end
  config.vm.define "glus2" do |g2|
    g2.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus2"
      unless File.exist?(file_to_disk2)
        vb.customize ['createhd', '--filename', file_to_disk2, '--size', size_disk]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk2]
    end
    g2.vm.network "private_network", ip: "10.10.2.12"
    g2.vm.hostname = "glus2.corp.itm.gt"
  end
  config.vm.define "glus0" do |g0|
    g0.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "glus0"
      unless File.exist?(file_to_disk0)
        vb.customize ['createhd', '--filename', file_to_disk0, '--size', size_disk]
      end
      vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', file_to_disk0]
    end
    g0.vm.network "private_network", ip: "10.10.2.10"
    g0.vm.hostname = "glus0.corp.itm.gt"
  end
end
