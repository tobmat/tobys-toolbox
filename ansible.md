### 

# Ansible

python-based software that automates software provisioning, configuration management, and application deployment.

# test inventory connections

ansible user\_setup -m setup -i inventory -o \| cut -d "" -f 1-3



# determine if ansible module is available:

ansible localhost -m &lt;module\_name&gt;



# debugging playbook runs:

ANSIBLE\_DEBUG=1 ansible-playbook &lt;playbook&gt;.yml

