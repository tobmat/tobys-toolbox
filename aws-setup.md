2 Instances in 2 AZ's

infosec-duo-dag-01

infosec-duo-dag-02



1 application elb

duo-dagELB- has CNAME entry in route 53 for access.genesyscloud.io



Cloudformation template:

[https://s3.us-east-2.amazonaws.com/gpc-cf-templates/duo\_dag\_instance.yml](https://s3.us-east-2.amazonaws.com/gpc-cf-templates/duo_dag_instance.yml)

Info: This template creates a rhel7.4 instance, installs docker-ce, and duo.   Installs letsencrypt\(NEED TO REMOVE\).  Does s3 copy of s3://gpc-cf-templates/scripts/duo.sh.  Runs this script to pull duo data tar from s3 bucket. Loads data into duo container.  This creates an active duo dag ready for use.



No longer needed:

Cert creation:

sudoletsencryptcertonly--standalone -d access.pureconnect.io -dwww.access.pureconnect.io

Note – may need to add--preferred-challenges tls-sni-01 flag



duo.sh script:

s3://gpc-cf-templates/scripts/duo.sh

This script is copied to /root with CF template above.  It runs in 2 different modes, import, and export:

export \(./root/duo.shexport\)- 

1. Export DUO config fromdagcontainer

2. Tar and zip config data

3. Copy config data to s3



import \(./root/duo.shimport\)-

1. PullDuo config tar file from s3.

2. Untarthese files

3. import new duo config todagcontainer

4. Stop / start duo access gateway



No longer needed:

Cert renewal:

[https://s3.us-east-2.amazonaws.com/atg-duo/duo\_renew\_cert.sh](https://s3.us-east-2.amazonaws.com/atg-duo/duo_renew_cert.sh)

This script is copied to /root with CF template above.  It runs in 2 different modes, primary, and non-primary:

Primary \(./root/duo\_renew\_cert.shp\)- This will testletsencryptcert to see if it's ready for renewal.  If ready for renewal it will do the following:

1. StopDUO DAG

2. Renew the cert

3. Start DUO DAG

4. Download DUO config

5. Copy new certs into DUO config

6. Tarletsencrypt, and duo config and push to s3

7. Copy updated config to DUO container

8. Bounce DUO service



Non-Primary \(./root/duo\_renew\_cert.shn\)-This will pull cert renewal info to any other servers.

It will do the following:

1. PullLetsencryptand Duo config tar files from s3.

2. Untarthese files

3. Upload new duo config

4. Stop / start duo access gateway



AdditionalNotes:

1. When instances are built they have everything they need to become the primary if needed.

2. Still need to test cert renewal script on primary when cert is ready to renew.

3. Currently only have 1 instance in load balancer.  Need to troubleshoot issue w



