# Ansible

## Ansible

python-based software that automates software provisioning, configuration management, and application deployment.

### test inventory connections

`ansible user_setup -m setup -i inventory -o | cut -d "" -f 1-3`

### test inventory

```text
ansible all -i <inventory name> --list-hosts
```

## determine if ansible module is available:

`ansible localhost -m <module_name>`

## debugging playbook runs:

`ANSIBLE_DEBUG=1 ansible-playbook <playbook>.yml`

### complex with\_items:

```text
  with_items:
     - { name: testuser1, uid: 1002, groups: "wheel, staff" }
     - { name: testuser2, uid: 1003, groups: staff }
```

