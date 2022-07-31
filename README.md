# Baseline Home Lab 

## The Machine Specs

![image](https://user-images.githubusercontent.com/993459/182042922-eea5f3e2-163f-499e-9fb6-48322ca3fc16.png)

Series	GTR5  
Ram Memory Installed Size	32 GB  
Operating System Fedora Linux  
CPU Model	Ryzen 9  
CPU Manufacturer AMD  
Human Interface Input	Mouse, Keyboard  
Hard Disk Description	HDD, 500GB Solid State Hard Drive  
Price: $719.00 US July 29, 2022 Amazon

## Software 
Ansible
MicroK8s - Kubernettes
Fedora 
KVM: Centos  
- Snapcraft - App Store from Conical
- Flathub - App Store
- Docker
- Portainer - Docker Portal
- BMON
- NMON
- Nginx Proxy Manager
- Dashy 
- Netdata


## kvm-cheats

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
# outside
sudo virsh list --all
virsh domiflist guestname
arp -e



#inside 
virsh domifaddr guestname --source agent
```

Virsh rename domain
```
virsh domrename currentname newname
```
```
mkdir /var/kvm/images
sudo virt-install \
--name dev-001 \
--disk path=/var/kvm/images/dev-001.qcow2,size=8 \
--vcpus 1 \
--ram 1024 \
--os-type linux \
--os-variant centos7.0 \
--graphics none \
--network bridge:virbr0 \
--console pty,target_type=serial -x 'console=ttyS0,115200n8 serial' \
--location 'http://mirror.centos.org/centos/7/os/x86_64/'
  
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

# KVM With Docker is the Real Deail

## Installation per distro
1. [centos 7](https://docs.docker.com/engine/install/centos/)
2. [Post Install](https://docs.docker.com/engine/install/linux-postinstall/)
> Note: Follow the instructions and do 'reboot' to get the systemctl on boot running

1. -d run as a process
2. --restart=always on reboot restart
```
# example
docker run --restart=always  -d -p 8080:80 --name web nginx 
---

