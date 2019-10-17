# © Copyright 2019 Hewlett Packard Enterprise Development LP

Vagrant.configure("2") do |config|
  config.vm.define :zfs_test do |zfs_test|
    zfs_test.vm.box = "centos/7"
    zfs_test.vm.network "public_network", dev: "virbr0"

    zfs_test.vm.provider :libvirt do |libvirt|
      libvirt.cpus = 4
      libvirt.cputopology sockets: 2, cores: 2, threads: 1
      libvirt.machine_arch = "x86_64"
      # libvirt.machine_virtual_size = "40G"
      libvirt.memory = 2048 # MB
      libvirt.numa_nodes = [
        { cpus: "0-1", memory: "1024" },
        { cpus: "2-3", memory: "1024" }
      ]
      9.times { libvirt.storage :file, size: "1G", type: "raw" }
    end

    zfs_test.vm.provision :ansible do |ansible|
      # ansible.become = true
      ansible.playbook = "playbook.yml"
      # ansible.verbose = "vvv"
    end
  end
end
