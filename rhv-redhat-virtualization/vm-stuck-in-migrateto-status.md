# VM stuck in MigrateTo status

#### Action Plan :&#x20;

\~ Check the qemu process , vdsclient and virsh on all host in cluster :&#x20;

`# vdsClient -s 0 list table | grep cfappaws02.us-east1a.genesyscloud.io `

`# ps aux|grep qemu-kvm |grep cfappaws02.us-east1a.genesyscloud.io `

`# virsh -r list | grep cfappaws02.us-east1a.genesyscloud.io `

\~ If there not any process for VM on all host run below query :&#x20;

\~ Prior running below query on RHVM please take engine backup :&#x20;

\>> refer : [https://protect-us.mimecast.com/s/gd7QCW6j8AixknQXHxlRit?domain=access.redhat.com](https://protect-us.mimecast.com/s/gd7QCW6j8AixknQXHxlRit?domain=access.redhat.com)&#x20;

\~ Run below command on RHVM for VM cfappaws02.us-east1a.genesyscloud.io&#x20;

\# /usr/share/ovirt-engine/dbscripts/engine-psql.sh -c "update vm\_dynamic SET status='0' where vm\_guid in (select vm\_guid from vm\_static where vm\_name='cfappaws02.us-east1a.genesyscloud.io');"&#x20;

\~ Then try to start the VM.&#x20;
