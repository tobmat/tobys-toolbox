# AWS Openshift

[https://aws.amazon.com/about-aws/whats-new/2016/06/red-hat-openshift-on-the-aws-cloud-quick-start-reference-deployment/](https://aws.amazon.com/about-aws/whats-new/2016/06/red-hat-openshift-on-the-aws-cloud-quick-start-reference-deployment/)

##### Add CNAME entry for elb:

for example: openshiftdev.oncaas.com

##### Add wildcard cert:

1. log into each master instance
2. copy wildcard.crt and wildcard.key to /etc/origin/master
3. update master config file \(/etc/origin/master/master-config.yaml\)
4. replace elb name for CNAME entry above.  Search public to find all entries
5. Add code to end of following sections: assetConfig, servingInfo

```
    namedCertificates:
      - certFile: wildcard.example.com.crt
        keyFile: wildcard.example.com.key
        names:
          - "openshift.example.com"6.
```

1. Restart atomic-openshift-master-api service

```
systemctl restart atomic-openshift-master-api
```

##### Add new users \(must run on all master instances\):

created a script to add new users from file:

```
##contents of new_users.sh

# add new users
while read line; do
  name=$(echo $line | cut -d "," -f 1)
  password=$(echo $line | cut -d "," -f 2)
  echo "add $name with password $password"
  #htpasswd -b /etc/origin/master/htpasswd $name $password
  htpasswd -D /etc/origin/master/htpasswd $name
done < $1

## contents of user.txt input file format

username,password

## add users to cluster-admin role

# add users to role
while read line; do
  name=$(echo $line | cut -d "," -f 1)
  echo "add $name to cluster-admin role"
  oadm policy add-role-to-user cluster-admin $name
done < $1
```

##### Helpful commands:

```
# validate user pw
htpasswd -v  /etc/origin/master/htpasswd admin

# delete user
oc delete identity htpasswd_auth:Brent.Rager
htpasswd -D /etc/origin/master/htpasswd Brent.Rager

# change pw
htpasswd /etc/origin/master/htpasswd admin

# get users
oc get users

# pass password on command line
htpasswd -b  /etc/origin/master/htpasswd admin
```

##### Login with command line tool:

```
oc login https://<openshift_url>:8443 -u username

# logout
oc logout
```



