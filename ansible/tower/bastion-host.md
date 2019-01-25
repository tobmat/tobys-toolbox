# Bastion Host

* SSH into tower and copy Bastion Host key, I put in /etc/ansible 
* give ownership of the key to awx and set proper permissions:

```text
sudo chown awx:awx /etc/ansible/private_key_file
chmod 600 /etc/ansible/private_key_file
```

* Add following variables to inventory, group , or instance you need to use bastion host on:

```text
---
ansible_ssh_common_args: '-o ProxyCommand="ssh -o StrictHostKeyChecking=no -W %h:%p -q user@jumphost"'
ansible_ssh_private_key_file: '/etc/ansible/private_key_file'
```

* Add credential for hosts you are going to access via jump server
* default playbook should have hosts: all and then control with limits in tower

