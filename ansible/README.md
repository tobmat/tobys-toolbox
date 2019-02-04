---
description: >-
  Python-based software that automates software provisioning, configuration
  management, and application deployment.
---

# Ansible

#### ansible-doc

Documentation plugin - see ansible-doc --help for more info

#### ad-hoc commands

```text
ansible <host reference> -i <inventory> -m <module> -a <module attributes>
# EXAMPLES
$ ansible everyone -m command -a 'id'

$ ansible everyone -m copy \
> -a 'content="This server is managed by Ansible.\n" dest=/etc/motd' --become

$ ansible everyone -m command -a 'cat /etc/motd'

# get list of ansible facts
$ ansible <instance or group from inventory> -m setup -a filter=ansible_local


```

#### test inventory connections

`ansible user_setup -m setup -i inventory -o | cut -d "" -f 1-3`

#### test inventory

```bash
ansible all -i <inventory name> --list-hosts
```

#### determine if ansible module is available:

`ansible localhost -m <module_name>`

#### debugging playbook runs:

`ANSIBLE_DEBUG=1 ansible-playbook <playbook>.yml`

#### complex with\_items:

```text
  with_items:
     - { name: testuser1, uid: 1002, groups: "wheel, staff" }
     - { name: testuser2, uid: 1003, groups: staff }
```

#### Set module parameter to default if variable isn't defined

```text
test: "{{ test_value | default(omit) }}"  
# if test_value doesn't exist parameter is set to default
# playbook example:
    - name: CVE-2016-5696 | Limit TCP challeng ACK limit
      sysctl:
        name: net.ipv4.tcp_challenge_ack_limit
        value: 999999999
        sysctl_set: yes
        sysctl_file: "{{ sysctl_file | default(omit) }}"

```

