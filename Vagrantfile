# © Copyright 2019 Hewlett Packard Enterprise Development LP

Vagrant.configure("2") do |config|
  config.vagrant.plugins = ["vagrant-cachier", "vagrant-libvirt"]
  config.vm.define :zfs_test do |zfs_test|
    zfs_test.vm.box = "centos/7"
    zfs_test.vm.network "public_network", dev: "virbr0"

    # By setting cache.scope to :box, downloaded packages will get stored on a
    # folder scoped to base boxes under your ~/.vagrant.d/cache. The idea is to
    # leverage the cache by allowing downloaded packages to be reused across
    # projects. The cached files will be stored under
    # $HOME/.vagrant.d/cache/some-box.
    if Vagrant.has_plugin?("vagrant-cachier")
      config.cache.scope = :box
    end

    zfs_test.vm.provider :libvirt do |libvirt|
      libvirt.cpus = 4
      libvirt.cputopology sockets: 2, cores: 2, threads: 1
      libvirt.machine_arch = "x86_64"
      # Image requires >= 40 GB HDD
      # libvirt.machine_virtual_size = "40G"
      libvirt.memory = 8192 # MB
      libvirt.numa_nodes = [
        { cpus: "0-1", memory: "4096" },
        { cpus: "2-3", memory: "4096" }
      ]
      3.times { libvirt.storage :file, size: "4G", type: "raw" }
    end

    zfs_test.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
      # ansible.skip_tags = ["run-tests"]
    end
  end
end
