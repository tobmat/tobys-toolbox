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

##### Install minishift:

```
yum install wget -y
cd /tmp
wget https://github.com/minishift/minishift/releases/download/v1.3.1/minishift-1.3.1-linux-amd64.tgz
tar -zxvf minishift-1.3.1-linux-amd64.tgz
mv minishift LICENSE README.adoc /usr/local/bin/.
minishift start
```

##### Activate oc:

```
minishift oc-env
export PATH="/root/.minishift/cache/oc/v1.5.1:$PATH"
```

Setup linux bridge to be able to access minishift from network:

```
virsh iface-bridge enp0s20f0 br0  # this creates the br0 bridge and update enp0s20f0 interface to point to 
                                  # the new bridge.  It creates the files in network-scripts and restarts network.
                                  
```

Replace default network on minishift vm with bridge interface:

```
virsh edit minishift

#search for default and replace with the following:
 <interface type='bridge'>
    <source bridge='br0'/>
 </interface>
 
```

Update openshift config to use public network:

```
minishift ssh
# determine public ip
sudo -i
vi /var/lib/minishift/openshift.local.config/master/master-config.yaml


```



