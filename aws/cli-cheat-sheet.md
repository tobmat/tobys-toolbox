# CLI Cheat Sheet

**Get List of all security groups by ID:**

`awsec2 describe-security-groups --query 'SecurityGroups[*].GroupId'  --output text |tr'\t' '\n' > all_sgs.txt`



**Get List of all SG used by instances:**

`awsec2 describe-instances --query 'Reservations[*].Instances[*].SecurityGroups[*].GroupId' --output text |tr'\t' '\n' | sort |uniq> used_sgs.txt`



**Get list of security groups not used by instances:**

`comm-23  <(awsec2 describe-security-groups --query 'SecurityGroups[*].GroupId'  --output text |tr'\t' '\n'| sort) <(awsec2 describe-instances --query 'Reservations[*].Instances[*].SecurityGroups[*].GroupId' --output text |tr'\t' '\n' | sort |uniq) > not_used.txt`



**Get list of security groups used by ELB load balancers:**

`awselbdescribe-load-balancers --query 'LoadBalancerDescriptions[*].SecurityGroups[*]' --no-paginate --output text |tr'\t' '\n' | sort |uniq> elb.txt`



**Get list of security groups rules for given security group id, format \(remove 1st line, join every 2 lines together, replace tabs and spaces with comma\):**

`awsec2 describe-security-groups --group-ids sg-0abf8c73 --output text |sed-n '1!p' |sed'N;s/\n/ /' |tr'\t' ',' |tr' ' ','`



**Use STS to assume another role:**

`awsstsassume-role --role-arnarn:aws:iam::515959988663:role/ansible-sts--role-session-name ansible-access --region us-east-1`



\# note just need to supply a region that supports this function

\# role-session-name is just name you give to the session

\# Can only be run from user or role that has trust established with role you want to assume

