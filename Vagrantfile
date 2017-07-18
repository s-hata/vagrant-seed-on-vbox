# -*- mode: ruby -*-
# vi: set ft=ruby :

Dotenv.load

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = ENV['BOX_NAME']
  config.vm.synced_folder ENV['SYNCED_DIR'], "/synced", mount_options: ["dmode=755", "fmode=755"]

  config.vm.define :server do |server|
    server.vm.hostname = ENV['VM_HOST_NAME']
    server.vm.network :private_network, ip: ENV['VM_IP_ADDRESS']
    server.vm.provider :virtualbox do |v, override|
      v.customize ["modifyvm", :id, "--memory", ENV['VM_MEMORY_SIZE']]
      v.customize ["modifyvm", :id, "--cpus", ENV['VM_CPU_COUNT']]
    end
  end 

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
  end

end
