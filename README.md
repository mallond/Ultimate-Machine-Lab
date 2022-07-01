# kvm-cheats

> I am using Fedora on a bare metal machine. KVM install went well! Too easy!

## World according to libvirtd
> ibvirt is an open-source API, daemon and management tool for managing platform virtualization. It can be used to manage KVM, Xen, VMware ESXi, QEMU and other virtualization technologies. These APIs are widely used in the orchestration layer of hypervisors in the development of a cloud-based solution.

Start Deamon
```
sudo systemctl status libvirtd
```

## World according to virsh
> The virtual shell, or virsh , is a flexible command-line utility for managing virtual machines (VMs) controlled by libvirt, which is a toolkit and API to manage virtualization platforms. It's the default management tool for Linux kernel-based virtual machines (KVMs), and it also supports Xen, VMware, and other platforms.

KVM Node info
```
sudo virsh nodeinfo
```

List --os-variant
```
osinfo-query os
```

List all domains
```
sudo virsh list --all
```

Virsh rename domain
```
virsh domrename currentname newname
```
```
sudo virt-install \
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
