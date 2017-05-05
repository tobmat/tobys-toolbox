# aws {#aws}

**aws command line setup**

**install \(**[**http://docs.aws.amazon.com/cli/latest/userguide/installing.html\#install-with-pip**](http://docs.aws.amazon.com/cli/latest/userguide/installing.html#install-with-pip)**\)**

sudo pip install awscli

**set the following as system variables**

Set this variabiles in /etc/profile.d/s3\_env\_var.sh

export AWS\_SECRET\_ACCESS\_KEY=

export AWS\_ACCESS\_KEY\_ID=

**s3 commands**

**online reference:**

[http://docs.aws.amazon.com/cli/latest/reference/s3/cp.html](http://docs.aws.amazon.com/cli/latest/reference/s3/cp.html)

**list containers**

aws s3 ls

**list files in given container**

aws s3 ls vst-vd

**copy local file to s3 container**

aws s3 cp vst-lpxyd02 s3://vst-vd/vst-lpxyd02.qcow2

**copy file from s3 to local**

aws s3 cp s3://vst-vd/vst-lpxyd02.qcow2 vst-lpxyd02.qcow2

**copy all files from a bucket to local**

aws s3 cp s3://mybucket . --recursive

**copy file from one s3 bucket to another**

copy: s3://mybucket/test.txt to s3://mybucket/test2.txt

**create bucket**

aws s3 mb s3://&lt;bucket name&gt;

**route53 commands**

**List all zones**

aws route53 list-hosted-zones

**List all records in zone**

aws route53 list-resource-record-sets --hosted-zone-id &lt;id&gt;

**S3 info**

Make a bucket public

1. click on bucket
2. expand the Permissions row
3. click "Add Bucket Policy"
4. copy/paste the snippet below into the text area.
5. change MY\_BUCKET\_NAME to the bucket you want
6. submit your changes

{

"Version": "2008-10-17",

"Statement": \[{

"Sid": "AllowPublicRead",

"Effect": "Allow",

"Principal": {

"AWS": "\*"

},

"Action": \[ "s3:GetObject" \],

"Resource": \[ "arn:aws:s3:::MY\_BUCKET\_NAME/\*" \]

}\]

}

