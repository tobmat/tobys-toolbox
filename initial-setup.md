Reference Links



[https://duo.com/docs/dag-linux](https://duo.com/docs/dag-linux)



Install steps:



 created an AD service account for DAG to use, set password to never expire \(atgservice\)



Linux DUO Access Gateway



Followed this documentation with some adjustments to use docker ce with rhel:

[https://duo.com/docs/dag-linux\#prerequisites](https://duo.com/docs/dag-linux#prerequisites)

  


1. Createdsshkey calledatg-dagto build instance with

2. Created a security group to address access needs listed in doc.  Made admin port only accessible via VPC IP range \(windows jump\)

| HTTP | TCP | 80 | 0.0.0.0/0 |  |
| :--- | :--- | :--- | :--- | :--- |
| SSH | TCP | 22 | 11.254.0.0/16 |  |
| Custom TCP Rule | TCP | 8443 | 11.254.0.0/16 |  |
| Custom TCP Rule | TCP | 636 | 11.254.0.0/16 |  |
| LDAP | TCP | 389 | 11.254.0.0/16 |  |
| HTTPS | TCP | 443 | 0.0.0.0/0 |  |
| All ICMP - IPv4 | All | N/A | 0.0.0.0/0 |  |





1. Create IAM role for DAG with full access policy for S3 \(This is to allow anydaginstance to upload configuration used to build futuredaginstances\)

2. Built server \(RHEL7.4\) in EC2 cloud hub VPC on private subnet using requirements listed in doc.  \(Question - What should we use for memory and disk?  Doc says 4GB or more and 20GB or more\)

3. Create application ELB security group:



| HTTPS | TCP | 443 | 0.0.0.0/0 |  |
| :--- | :--- | :--- | :--- | :--- |
| All ICMP - IPv4 | All | N/A | 0.0.0.0/0 |  |



1. Create application ELB:

Internet-facing, in both AZ's on public network, security group created above, deletion protection enabled, target group HTTPS, stickiness enabled for 8 hours to match DAGs, add ELB instances.



1. Added DNS entry in route53:  CNAME record[access.genesyscloud.io](https://access.genesyscloud.io/)pointing to duo-dagELB.

2. Followed Centos7 instructions to install docker \(Note -Redhatinstructions required paid EE version of docker\)



`sudoyum installwgetyum-utils-y`

`sudoyum-config-manager --add-repo`[`https://download.docker.com/linux/centos/docker-ce.repo`](https://download.docker.com/linux/centos/docker-ce.repo)`&> /dev/null`

`sudoyum-config-manager --enablerhui-REGION-rhel-server-extrasrhui-REGION-rhel-server-optional &> /dev/null`

`sudoyum installcertbot-nginx-y &> /dev/null`

`sudoyummakecachefast &> /dev/null`

`sudoyum update -y &> /dev/null`

`sudoyum install docker-ce-y`

`sudosystemctlenabledocker.service`

`sudosystemctlstart docker`

`sudousermod-aGdocker ec2-user &> /dev/null`

`wget-O- "`[`https://github.com/docker/compose/releases/download/1.13.0/docker-compose-$(uname`](https://github.com/docker/compose/releases/download/1.13.0/docker-compose-$%28uname)`-s)-$(uname-m)" > ./docker-compose`

`chmod+x ./docker-compose`

`sudomv ./docker-compose /usr/local/bin/`

`wget--content-disposition`[`https://dl.duosecurity.com/access-gateway-latest.yml`](https://dl.duosecurity.com/access-gateway-latest.yml)

`  docker-compose -p access-gateway -f access-gateway* up -d`



From DAG Admin Console - accessed from 8443 from AWS windows jump



Authentication Source:



1. Get IP addresses of AWS domain controllers and use this format on Authentication Source tab

ldap://11.254.1.234,ldap://11.254.2.94



1. Transport type : clear

2. Attributes / search attributes: distinguishedName,mail,sAMAccountName,userPrincipalName

3. Search base: OU=users,OU=pureconnect,DC=pureconnect,DC=cloud

4. Provide AD service account username and pw



Launcher

1. Create a Duo Access Gateway application in the Duo Admin Panel  \(This is done by Infosec \(Kitch\)\)

2. Load DAG keys,apiinfo





Applications

1. Create a SAML application in the Duo Admin Panel. \(This is done by Infosec\)

2. Upload configuration file provided by Infosec

3. Download XML metadata for AWS setup

4. Follow these instructions for AWS setup:[https://duo.com/docs/aws](https://duo.com/docs/aws)



Settings

1. Change Admin Password

2. Internet – upload wildcard cert info





From DAG instance

  \# installawscli

`sudo yum install`[`http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`](http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm)`-y`

`sudoyum install python-pip -y`

`sudo pip install awscli`



 \# download duo.sh script to pull config from dag container and upload to s3

`sudo aws s3 cp s3://gpc-cf-templates/scripts/duo.sh /root/duo.sh`

`sudo chmod a+x /root/duo.sh`

`sudo ./root/duo.sh export > /tmp/duo.output`

