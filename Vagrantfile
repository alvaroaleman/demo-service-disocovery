# -*- mode: ruby -*-
# vi: set ft=ruby :
# Based on http://thornelabs.net/2014/11/13/multi-machine-vagrantfile-with-shorter-cleaner-syntax-using-json-and-loops.html
boxes = [
  {
    :name => 'demo-service-discovery'
  }
]


# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  boxes.each do |box|
    config.vm.define box[:name] do |config|
      # The most common configuration options are documented and commented below.
      # For a complete reference, please see the online documentation at
      # https://docs.vagrantup.com.

      # Every Vagrant development environment requires a box. You can search for
      # boxes at https://atlas.hashicorp.com/search.
      config.vm.box = "centos/7"
      config.vm.hostname = box[:name]
      config.vm.synced_folder '.', '/home/vagrant/sync', disabled: true
      config.vm.synced_folder '.', '/vagrant', id: 'vagrant-root', disabled: true

      config.vm.provision :ansible do |ansible|
        ansible.playbook = 'playbook.yml'
        ansible.raw_arguments = '--diff'
        if ENV['CHECKMODE'] == '1'
            ansible.raw_arguments << '--check'
        end
      end

      config.vm.provider :libvirt do |lv|
          lv.cpus = 2
          lv.memory = 2048
          lv.keymap = "de"
          lv.nested = true
        end
      config.vm.provider :virtualbox do |v|
        v.customize 'pre-boot', ['modifyvm', :id, '--nictype1', 'virtio']
        v.customize [ 'modifyvm', :id, '--memory', '1024', '--cpus', '2' ]
      end

    # End box configuration
    end

  # End boxes loop
  end

# End config
end
