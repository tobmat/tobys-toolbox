**To setup ansible to run with azure on RHEL:**

Install ansible engine

`sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release`

`sudo yum install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y`

`sudo yum install -y python-pip python-wheel`

`sudo pip install ansible[azure]`



**Export service principle variables:**

`export AZURE_SUBSCRIPTION_ID=<subscription id>`

`export AZURE_CLIENT_ID=<client id>`

`export AZURE_SECRET=<secret>`

`export AZURE_TENANT=<tenant>`



