# aws {#aws}

### **aws command line setup \(awscli\)**

* **install \(**[**http://docs.aws.amazon.com/cli/latest/userguide/installing.html\#install-with-pip**](http://docs.aws.amazon.com/cli/latest/userguide/installing.html#install-with-pip)**\)**

`sudo pip install awscli`

* **set the following as system variables** in /etc/profile.d/s3\_env\_var.sh

export AWS\_SECRET\_ACCESS\_KEY=

export AWS\_ACCESS\_KEY\_ID=

#### iam commands

###### List security groups that have wide open ip rules and only return certain values with query:

```
aws ec2 describe-security-groups --filters Name=ip-permission.cidr,Values='0.0.0.0/0' --query 'SecurityGroups[*].{Name:GroupName,VPCID:VpcId,SecurityGroupName:GroupId}'
```

###### List Users in text format:

```
aws iam list-users --output text  # other valid options are table, and json(default)
```

#### **route53 commands**

###### **List all zones:**

`aws route53 list-hosted-zones`

###### **List all records in zone:**

`aws route53 list-resource-record-sets --hosted-zone-id <id>`

#### 



