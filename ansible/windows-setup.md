# Windows Setup

## windows machines

1. Set-ExecutionPolicy Bypass (or setup to use certificates)
2. Enable-PSRemoting -Force
3. winrm set winrm/config/service @{AllowUnencrypted="true"}
4. AWS - add security group rule to allow traffic on 5985

## ansible server

1. yum -y install gcc python-devel krb5-devel krb5-workstation
2. pip install [https://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm](https://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm)
3. pip install python-kerberos
4. pip install requests-kerberos

### create windows inventory file containing the following:

```
[windows]
win-jump-east02.cloudhub.local

[windows:vars]
 ansible_ssh_user=toby.matherly@CLOUDHUB.LOCAL
 #ansible_ssh_pass=passwordhere
 ansible_ssh_port=5985
```

### Change /etc/resolv.conf to use same DNS server as windows server you are trying to access (for AWS)

### Update /etc/krb5.conf and change the following sections: (kdc is pointing to domain controller of windows instance

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

### Create a keberos ticket:

```
kinit toby.matherly@CLOUDHUB.LOCAL
```

### Validate ticket:

```
klist
Ticket cache: KEYRING:persistent:0:0
Default principal: toby.matherly@CLOUDHUB.LOCAL

Valid starting       Expires              Service principal
05/19/2017 15:19:46  05/20/2017 01:19:46  krbtgt/CLOUDHUB.LOCAL@CLOUDHUB.LOCAL
    renew until 05/26/2017 15:19:43
```

### Test winrm:

```
ansible win-jump-east02.cloudhub.local -m win_ping -i win-inventory
win-jump-east02.cloudhub.local | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

## Basic windows playbook to run powershell script:

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

### Troubleshooting

#### ansible kerberos hangs on winrm connection

This can be resolved by installing **pexpect** with pip
