If additional packages on tower nodes are needed.

#### **From each Tower node:**

\# log in as root

`sudo -i`

\# access ansible virtual environment

`. /var/lib/awx/venv/ansible/bin/activate`

\# pip install needed packages

`pip install <packagename>`

**Nuage Support:**

`pip install vspk`

note: do not install anything in /var/lib/awx/venv/awx/lib venv.  Not needed and NOT supported by redhat



#### Ansible Azure modules:

`Ansible venv:`

`1. su -`

`2. cd /var/lib/awx/venv/ansible/bin`

`3. source activate`

`4. pip install ansible[azure] --upgrade --force`

`5. deactivate`

