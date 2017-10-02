### Setup for windows

#### windows machines

1. Set-ExecutionPolicy Bypass \(or setup to use certificates\)

2. Enable-PSRemoting -Force

3. winrm set winrm/config/service @{AllowUnencrypted="true"}

4. AWS - add security group rule to allow traffic on 5985

#### ansible server

1. yum -y install gcc python-devel krb5-devel krb5-workstation
2. pip install [https://github.com/diyan/pywinrm/archive/master.zip\#egg=pywinrm](https://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm)
3. pip install python-kerberos
4. pip install requests-kerberos

##### create windows inventory file containing the following:

```
[windows]
win-jump-east02.cloudhub.local

[windows:vars]
 ansible_ssh_user=toby.matherly@CLOUDHUB.LOCAL
 #ansible_ssh_pass=passwordhere
 ansible_ssh_port=5985
```

##### Change /etc/resolv.conf to use same DNS server as windows server you are trying to access \(for AWS\)

##### Update /etc/krb5.conf and change the following sections: \(kdc is pointing to domain controller of windows instance

```
[realms]
 CLOUDHUB.LOCAL = {
  kdc = win-ct1jf3e6fce.cloudhub.local
  admin_server = win-ct1jf3e6fce.cloudhub.local
 }

[domain_realm]
 .cloudhub.local = CLOUDHUB.LOCAL
 cloudhub.local = CLOUDHUB.LOCAL
```

##### Create a keberos ticket:

```
kinit toby.matherly@CLOUDHUB.LOCAL
```

##### Validate ticket:

```
klist
Ticket cache: KEYRING:persistent:0:0
Default principal: toby.matherly@CLOUDHUB.LOCAL

Valid starting       Expires              Service principal
05/19/2017 15:19:46  05/20/2017 01:19:46  krbtgt/CLOUDHUB.LOCAL@CLOUDHUB.LOCAL
    renew until 05/26/2017 15:19:43
```

##### Test winrm:

```
ansible win-jump-east02.cloudhub.local -m win_ping -i win-inventory
win-jump-east02.cloudhub.local | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

#### Basic windows playbook to run powershell script:

```
- name: test
  hosts: windows

  vars_prompt:
    - name: "ansible_ssh_pass"
      prompt: "windows password"
      private: yes

  tasks:
    - name: run test script
      script: test_script.ps1
```

### Ansible Tower

#### Bastion Host

* SSH into tower and copy Bastion Host key, I put in /etc/ansible 
* give ownership of the key to awx and set proper permissions:

```
sudo chown awx:awx /etc/ansible/private_key_file
chmod 600 /etc/ansible/private_key_file
```

* Add following variables to inventory, group , or instance you need to use bastion host on:

```
---
ansible_ssh_common_args: '-o ProxyCommand="ssh -o StrictHostKeyChecking=no -W %h:%p -q user@jumphost"'
ansible_ssh_private_key_file: '/etc/ansible/private_key_file'
```

* Add credential for hosts you are going to access via jump server
* default playbook should have hosts: all and then control with limits in tower

#### Import existing inventories / variables into tower

* see tips and tricks below
* create empty inventory in tower
* On tower server copy an existing inventory structure in inventory/ directory
* execute this command:

```
tower-manage inventory_import --source=inventory/ --inventory-name="<inventory name>"
```

#### Tips and Tricks

[http://docs.ansible.com/ansible-tower/latest/html/administration/tipsandtricks.html](http://docs.ansible.com/ansible-tower/latest/html/administration/tipsandtricks.html)



