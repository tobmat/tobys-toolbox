# Minishift

[minishift install](https://docs.openshift.org/latest/minishift/getting-started/installing.html)

I built minishift on centos7, running KVM.  Following the instructions above.

##### Install libvirt and qemu-kvm:

```
yum install libvirt virt-manager bridge-utils qemu-kvm
systemctl enable libvirtd
systemctl start libvirtd
```

##### Install and test docker machine \(see [here](https://github.com/dhiltgen/docker-machine-kvm#quick-start-instructions) for more details\):

    curl -L https://github.com/docker/machine/releases/download/v0.12.2/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine && \
    chmod +x /tmp/docker-machine && \
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine

    rmmod kvm_intel
    rmmod kvm
    modprobe kvm
    modprobe kvm_intel

    Test install:
    docker-machine start myengine0




