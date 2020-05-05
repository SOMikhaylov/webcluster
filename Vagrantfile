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
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|
          
          box.vm.synced_folder '.', '/vagrant', disabled: true
          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s

          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          case boxname.to_s
          when "db3"
            box.vm.provision "ansible" do |ansible|
                  ansible.playbook = "provision.yml"
                  ansible.limit = "all"
                  ansible.groups = {
                  "db" => ["db[1:3]"],
                  }
            end
          end
      end
  end
end
