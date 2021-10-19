# Vault

We will store sensitive data using Ansible Vault.

**Steps to setup vault in repo:**

`ansible-vault create roles/<rolename>/vars/vault.yml`

**Example content:**

`---`

`vault_password: password`

**To follow best practices:**

1. Prefix all variable invault.ymlwith vault\_
2. Reference all vault variables in non-encrypted variable files.

**Example content:**\
`---`

`Password: "{{vault_password}}"`

**To use in playbook:**

`tasks:`

`-include_vars: "roles/<rolename>/vars/vault.yml"`

**To run playbook:**

`# enter vault password when prompted  `\
`ansible-playbook <playbook>.yml--ask-vault-pass`

OR

\# create a temporary vault file to store password for development. Do NOT make part of repo!

`ansible-playbook <playbook>.yml--vault-id <vault_file>`

**To use in Tower:**

1. Create new tower vault credential using same vault password. (This has been created and is called vault)
2. Add it an another creditional in any templates that need it.

**Additional Vault commands:**

Edit Vault file:

`ansible-vault edit roles/<rolename>/vars/vault.yml`
