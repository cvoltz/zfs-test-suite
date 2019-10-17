# Description

Files to create a CentOS VM, using Vagrant and the libvirt provider, which runs
the ZFS test suite.

To create the VM:
```
vagrant up --provider=libvirt
```

To connect to the running VM:
```
vagrant ssh
```

To get rid of the VM:
```
vagrant destroy
```

The VM is provisioned using Ansible. Ansible must be installed on the host. If
the `playbook.yml` file is updated, run
```
vagrant provision
```
to reprovision the VM. For debugging purposes (or to more quickly re-run Ansible
on the VM), run:
```
./run-ansible
```

# Useful links

* [Ansible](https://ansible.com)
  * [Ansible documentation](https://docs.ansible.com)
* [Vagrant](https://www.vagrantup.com)
  * [Vagrant Ansible Provisioner docs](https://www.vagrantup.com/docs/provisioning/ansible.html)
* [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt) provider
* [zfs](https://github.com/zfsonlinux/zfs) GitHub repo
  * [spl](https://github.com/zfsonlinux/spl) GitHub repo
  * [Building ZFS](https://github.com/zfsonlinux/zfs/wiki/Building-ZFS)
  * [ZFS Test Suite](https://github.com/zfsonlinux/zfs/tree/master/tests)

# Contributors

[Christopher Voltz](mailto:christopher.voltz@hpe.com)

# Copyright

© Copyright 2019 Hewlett Packard Enterprise Development LP
