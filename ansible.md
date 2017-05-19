### Setup for windows

#### windows machines

1. Set-ExecutionPolicy Bypass \(or setup to use certificates\)

2. Enable-PSRemoting -Force

3. winrm set winrm/config/service @{AllowUnencrypted="true"}

4. AWS - add security group rule to allow traffic on 5985

#### ansible server

yum -y install python-devel krb5-devel krb5-libs krb5-workstation

1. yum -y install gcc python-devel krb5-devel krb5-workstation



pip install pywinrm\[kerberos\]

2. pip install https://github.com/diyan/pywinrm/archive/master.zip\#egg=pywinrm



pip install python-kerberos

yum install python-kerberos



pip install requests-kerberos



create windows inventory file containing the following 

```
[windows]
win-jump-east02.cloudhub.local

[windows:vars]
 ansible_ssh_user=toby.matherly@CLOUDHUB.LOCAL
 #ansible_ssh_pass=passwordhere
 ansible_ssh_port=5985
 ansible_connection=winrm
```

Change /etc/resolv.conf to use same DNS server as windows server you are trying to access \(for AWS\)

