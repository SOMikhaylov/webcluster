# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :db1 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.11',
  },
  :db2 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.12',
  },
  :db3 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.13',
  },
  :app1 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.21',
  },
  :app2 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.22',
  },
  :lb1 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.31',
  },
  :lb2 => {
        :box_name => "centos/8",
        :ip_addr => '192.168.1.32',
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|
          
          box.vm.synced_folder '.', '/vagrant', disabled: true
          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s

          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          case boxname.to_s
          when "lb2"
            box.vm.provision "ansible" do |ansible|
                  ansible.playbook = "provision.yml"
                  ansible.limit = "all"
                  ansible.groups = {
                  "db" => ["db[1:3]"],
                  "app" => ["app[1:2]"],
                  "lb" => ["lb[1:2]"],
                  }
            end
          end
      end
  end
end
