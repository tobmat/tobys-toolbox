# Upgrade

**From Linux Utility instance:**

`cd ansible-tower-setup-<tower_version> # example -ansible-tower-setup-3.2.1`

**Run setup command with backup \(-b\) flag:** 

```text
./setup.sh -b # Will only run on one of the tower instances and will copy the backup to the local directory.
```

**Upgrade Tower instance:**

Copy URL for latest version from here:  
[http://releases.ansible.com/ansible-tower/setup/](http://releases.ansible.com/ansible-tower/setup/)

`cd /home/ec2-user`

`wget`[`http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz`](http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz)

**Extract tar file:**

`tar -xvzf ansible-tower-setup-latest.tar.gz`

`cd ansible-tower-setup-<tower_version>`

**Copy inventory file to new directory:**

`cp../ansible-tower-setup-<current_tower_version>/inventory .`

**Run setup.sh script:**

`./setup.sh`

**Validate Tower Upgrade:**

1. Login to tower UI
2. Go to settings
3. Select 'About Tower'
4. Confirm new Tower Version is reflected

