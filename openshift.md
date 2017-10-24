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

##### Setup linux bridge to be able to access minishift from network:

```
virsh iface-bridge enp0s20f0 br0  # this creates the br0 bridge and update enp0s20f0 interface to point to 
                                  # the new bridge.  It creates the files in network-scripts and restarts network.

#review bridge
brctl show
```

##### Replace default network on minishift vm with bridge interface:

```
virsh edit minishift

#search for default and replace with the following:
 <interface type='bridge'>
    <source bridge='br0'/>
 </interface>
```

##### Update openshift config to use public network:

```
minishift ssh
# determine public ip
ip a # find ip on public network
sudo -i
vi /var/lib/minishift/openshift.local.config/master/master-config.yaml

# find and replace this values with public ip
  masterPublicURL: https://192.168.88.233:8443
  publicURL: https://192.168.88.233:8443/console/
masterPublicURL: https://192.168.88.233:8443
  assetPublicURL: https://192.168.88.233:8443/console/
  masterPublicURL: https://192.168.88.233:8443
  subdomain: 192.168.88.233.nip.io

exit
exit
minishift stop
minishift start
```

##### Webhooks:

For testing in lab that is not internet facing I used [ultrahook.](http://www.ultrahook.com/)

```
# it is a gem so to prep centos7 I installed the following

yum install ruby-devel ruby gcc -y

# follow install instructions on site

ultrahook testhook https://192.168.88.233:8443/oapi/v1/namespaces/wfproject/buildconfigs/helloworld/webhooks/53ac93c7cb5d214c/github

# this will create a webhook and provide the url to put in at github
# the url you use is from openshift project created
```

##### Troubleshooting

The project in the book to launch the docker image for tomcat was failing / restarting when I tried to bring it up.

```
oc status -v   # this command provides troubleshooting steps.  In this case the default security policy
               # prevented containers from being run as root user which happens to be required for tomcat8.

#They suggested running this command:
#oadm policy add-scc-to-user anyuid -n tomcat8 -z default

# The problem is oadm is not available in minishift but you can use the following command instead:
oc adm policy add-scc-to-user anyuid -n tomcat8 -z default

#NOTE - need to use this login first:
oc login -u system:admin
```

# AWS Openshift

[https://aws.amazon.com/about-aws/whats-new/2016/06/red-hat-openshift-on-the-aws-cloud-quick-start-reference-deployment/](https://aws.amazon.com/about-aws/whats-new/2016/06/red-hat-openshift-on-the-aws-cloud-quick-start-reference-deployment/)

##### Add CNAME entry for elb:

for example: openshiftdev.oncaas.com

##### Add wildcard cert:

1. log into each master instance
2. copy wildcard.crt and wildcard.key to /etc/origin/master
3. update master config file \(/etc/origin/master/master-config.yaml\)
4. replace elb name for CNAME entry above.  Search public to find all entries
5. Add code to end of following sections: assetConfig, servingInfo

```
    namedCertificates:
      - certFile: wildcard.example.com.crt
        keyFile: wildcard.example.com.key
        names:
          - "openshift.example.com"6.
```

1. Restart atomic-openshift-master-api service

```
systemctl restart atomic-openshift-master-api
```

##### Add new users \(must run on all master instances\):

created a script to add new users from file:

```
##contents of new_users.sh

# add new users
while read line; do
  name=$(echo $line | cut -d "," -f 1)
  password=$(echo $line | cut -d "," -f 2)
  echo "add $name with password $password"
  #htpasswd -b /etc/origin/master/htpasswd $name $password
  htpasswd -D /etc/origin/master/htpasswd $name
done < $1

## contents of user.txt input file format

username,password

## add users to cluster-admin role

# add users to role
while read line; do
  name=$(echo $line | cut -d "," -f 1)
  echo "add $name to cluster-admin role"
  oadm policy add-role-to-user cluster-admin $name
done < $1
```

##### Helpful commands:

```
# validate user pw
htpasswd -v  /etc/origin/master/htpasswd admin

# delete user
oc delete identity htpasswd_auth:Brent.Rager
htpasswd -D /etc/origin/master/htpasswd Brent.Rager

# change pw
htpasswd /etc/origin/master/htpasswd admin

# get users
oc get users
```

##### Login with command line tool:

```
oc login https://<openshift_url>:8443 -u username
```



