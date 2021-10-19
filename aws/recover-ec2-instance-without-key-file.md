# Recover EC2 Instance without key file

Stop the lost pem file instance. Remember not to terminate instance but to stop it.

1. GotoEBS volumes, select the root volume of the lost pem file instance and detach.
2. Now again select the detached volume and this time you have to attach this volume to another instance.
3. Login to instance you attached volume to.
4. Execute below commands:

`>lsblk # determine the device name`

`> file -s /dev/xvdf`

`>sudo mkdir <mount_dir>`

`> rpm –q nfs-utils`

`>sudo yum install nfs-utils -y # I needed this in order to mount the volume`

`> mount –o nouuid /dev/xvdf2 <mount_dir> # had conflict with uuid so added the –o flag`

`> update <mount_dir>/home/ec2-user/.ssh/authorized_keys with available key`

`>umount <mount_dir>`

AWS Console

1. Detach the secondary volume from instance.
2. Again attach the volume back to our recovery instance. Start the instance.
3. Access instance with newly added key.
