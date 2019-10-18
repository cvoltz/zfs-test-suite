# Description

Files to create a CentOS VM, using Vagrant and the libvirt provider, which run
the [SPLAT](https://github.com/zfsonlinux/spl/tree/spl-0.7-release) and [ZFS
Test](https://github.com/zfsonlinux/zfs/tree/master/tests) suites which are
provided as part of [SPL](https://github.com/zfsonlinux/spl) and
[ZFS](https://github.com/zfsonlinux/zfs).

# Dependencies

Required:
* [Ansible](https://ansible.com) >= 2.8.5
* [centos/7](https://app.vagrantup.com/centos/boxes/7) Vagrant box >= v1905.1
* [Vagrant](https://www.vagrantup.com) >= 2.2.6
* [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt) Vagrant provider >= 0.0.45

Optional:
* [vagrant-cachier](https://github.com/fgrehm/vagrant-cachier) >= 1.2.1

Tested with [SPL](https://github.com/zfsonlinux/spl) and [ZFS](https://github.com/zfsonlinux/zfs) 0.7.13.

These steps *may* be sufficient to setup a CentOS 7 system:
```
sudo yum install -y https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.rpm
sudo yum install -y epel-release
sudo yum install -y ansible
vagrant plugin install vagrant-libvirt
```

# Operating the VM

### Create the VM

```
vagrant up --provider=libvirt
```
or
```
./start
```

### Destroy the VM

```
vagrant destroy
```

### Connect to running VM

```
vagrant ssh
```

### Re-provision the VM

When it is started, the VM is automatically provisioned using Ansible. Ansible
must already be installed on the host.

If the `playbook.yml` file is updated, re-provision the VM by running:
```
vagrant provision
```
For debugging purposes (or to more quickly re-run Ansible on the VM), run:
```
./run-ansible
```

### Get test results
```
./get-results
```

`/var/tmp/test_results` in the VM will be copied to `test_results` in the
current directory. The output of running `zfs-tests.sh` will be in
`test_results/current/tests.log` along with the results of the last run.
`get-results` can be run repeatedly without worrying about losing previous
results as the ZFS test suite puts the results for each run in a directory whose
name is a basic format combined date and 24 hour time ISO 8601 timestamp (e.g.,
`20191022T020443`).

# Useful links

* [Ansible documentation](https://docs.ansible.com)
* [Vagrant Ansible Provisioner docs](https://www.vagrantup.com/docs/provisioning/ansible.html)
* [Building ZFS](https://github.com/zfsonlinux/zfs/wiki/Building-ZFS)
* [Custom Packages](https://github.com/zfsonlinux/zfs/wiki/Custom-Packages)
* [bb-bootstrap.sh](https://github.com/zfsonlinux/zfs-buildbot/blob/master/scripts/bb-bootstrap.sh)
* [bb-dependencies.sh](https://github.com/zfsonlinux/zfs-buildbot/blob/master/scripts/bb-dependencies.sh)
* [tests/functional/delegate/setup.ksh](https://github.com/zfsonlinux/zfs/blob/master/tests/zfs-tests/tests/functional/delegate/setup.ksh)

# Contributors

[Christopher Voltz](mailto:christopher.voltz@hpe.com)

# Copyright

© Copyright 2019 Hewlett Packard Enterprise Development LP
