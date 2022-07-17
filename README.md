# kvm-cheats

> I am using Fedora on a bare metal machine. KVM install went well! Too easy!

## World according to libvirtd
> ibvirt is an open-source API, daemon and management tool for managing platform virtualization. It can be used to manage KVM, Xen, VMware ESXi, QEMU and other virtualization technologies. These APIs are widely used in the orchestration layer of hypervisors in the development of a cloud-based solution.

> Install Fedora

core
```
sudo dnf -y install bridge-utils libvirt virt-install qemu-kvm
```
extra
```
sudo dnf install libvirt-devel virt-top libguestfs-tools guestfs-toolsd
```

Start Deamon
```
sudo systemctl status libvirtd
```
```
sudo systemctl status libvirtd
```

Connect To Libvirt with Virsh
```
sudo virsh
```
> GOTCHA - Although, virsh may give feedback, for example virsh list --all, without sudo you may not see the whole picture. virsh is a sudo type of tool but does not always tell you that. When in doubt sudo or 'sudo virsh' and run your commands

## World according to virsh
> The virtual shell, or virsh , is a flexible command-line utility for managing virtual machines (VMs) controlled by libvirt, which is a toolkit and API to manage virtualization platforms. It's the default management tool for Linux kernel-based virtual machines (KVMs), and it also supports Xen, VMware, and other platforms.

KVM Node info
```
virsh nodeinfo
```

List --os-variant
```
osinfo-query os
```

List all domains
```
virsh list --all
```

Find IP Address of a domain
```
virsh list
virsh domifaddr rhel7
```

Virsh rename domain
```
virsh domrename currentname newname
```
```
virt-install \
  --name centos7 \
  --description "Test VM with CentOS 7" \
  --ram=1024 \
  --vcpus=2 \
  --os-type=Linux \
  --os-variant=centos7.0 \
  --disk path=/var/lib/libvirt/images/centos7.qcow2,bus=virtio,size=10 \
  --graphics none \
  --location /home/dmallon/iso-images/CentOS-7-x86_64-DVD-2009.iso \
  --network bridge:virbr0 \
  --console pty,target_type=serial -x 'console=ttyS0,115200n8 serial'
  
```
```
virt-install \
--name centos7 \
--ram 1024 \
--disk path=./centos7.qcow2,size=8 \
--vcpus 1 \
--os-type linux \
--os-variant centos7 \
--network bridge=virbr0 \
--graphics none \
--console pty,target_type=serial \
--location 'http://mirror.i3d.net/pub/centos/7/os/x86_64/' \
--extra-args 'console=ttyS0,115200n8 serial'
```
### Virsh Snapshots

List
```
virsh snapshot-list name-of-vm
```

Create
```
virsh snapshot-create-as --domain nameOfVM --name nameOfVM_snap --description "snap before patch on 4Feb2018"
```

Delete
```
virsh snapshot-delete --domain nameOfVM --snapshotname nameOfVM_snap
```
