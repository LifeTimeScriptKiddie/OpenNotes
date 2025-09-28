---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/clouds/aws/aws-tools/","noteIcon":"","created":"2025-04-15T14:11:19.592-04:00"}
---





## awscli
```
apt install awscli
curl "hRps://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update


aws s3 --endpoint-url


aws configure
aws s3 --endpoint-url http://s3.bucket.htb ls


aws s3 --endpoint-url http://s3.bucket.htb ls s3://adserver
```

## aws-recon
```
https://github.com/joshlarsen/aws-recon


```
## Pacu
```
pip3 install -U pip
pip3 install -U pacu
pacu

or

sudo apt install pacu


https://github.com/RhinoSecurityLabs/pacu

Need credentials

https://github.com/RhinoSecurityLabs/pacu/wiki/Quick-Start-Guide

 2186  git clone https://github.com/RhinoSecurityLabs/pacu
 2190  python3 -m venv my_env
 2192  source ./my_env/bin/activate
 2194  pip install -r requirements.txt
 2207  ./install.sh
 2212  pip3 install pacu
 2213  pacu


```

## AWSBucketDump
Targets the entire bucket. 
Needs Tailoring python code for specific websites. 
```
## Tool installation:
git clone https://github.com/jordanpotti/AWSBucketDump.git

## modify the .py file to matching your python version

## Run the tool:
cd AWSBucketDump
python AWSBucketDump.py -l BucketNames.txt -g interesting_Keywords.txt -D -m 500000 -d 1 
```

## CloudFox
Need profile
```
aws configure -profile

git clone https://github.com/BishopFox/cloudfox.git
cd ./cloudfox
go build .
./cloudfox

When creating the credentials for the tool, add
“arn:aws:iam::aws:policy/SecurityAudit” policy access to the
cloudfox user


For the latest update visit the repo:
hRps://github.com/BishopFox/cloudfox


cloudfox aws --profile [profile-name] all-checks



```

## Cred Scanner
Works on local host
```
git clone https://github.com/disruptops/cred_scanner.git
cd cred_scanner
pip install -r ./requirements.txt
Using the tool:
create 2 files for the tesLng with AWS keys
python cred_scanner.py --path /abc/abc

```
## Prowler

Need credentials
```
git clone https://github.com/prowler-cloud/prowler
cd prowler
poetry shell
poetry install
python prowler.py –v
Using the tool:
prowler aws
For the latest update visit the repo:
https://github.com/prowler-cloud/prowler

```

## CloudBrute
```
git clone https://github.com/0xsha/CloudBrute.git
cd CloudBrute
nano config/config.yaml
Add API key from https://ipinfo.io/
go build -o CloudBrute main.go
Using the tool:
./CloudBrute -d flaws.cloud -k flaw -m storage -t 80 -T 10 -w "./data/storage_small.txt"
./CloudBrute -d flaws.cloud -k flaws -w data/storage_large.txt
./CloudBrute -d flaws.cloud -k flaws -a -w data/storage_small.txt
./CloudBrute -d flaws.cloud -k flaws -a -w data/storage_small.txt -m app
./CloudBrute -d flaws.cloud -k flaws -a -w data/app_small.txt -m app
./CloudBrute -d github.com -k github -m storage -t 80 -T 10 -w "./data/storage_small.txt"
```

## Dufflebag

## Enumerate IAM
```
git clone hRps://github.com/andresriancho/enumerate-iam.git
cd enumerate-iam/
pip install -r requirements.txt
Using the tool:
./enumerate-iam.py --access-key <REDACTED> --secret-key <REDACTED>


```

https://www.y-security.de/news-en/hack-the-box-blacksky-cloud-hacking-labs-hailstorm/
-  **[aws-cli](https://github.com/aws/aws-cli)**: Provides a unified command line interface to Amazon Web Services
-  **[aws-cli reference](https://docs.aws.amazon.com/cli/latest/reference/index.html#cli-aws)**: Command reference of aws-cli and useful information about resources
-  [**Prowler**](https://github.com/prowler-cloud/prowler): Prowler is an Open Source security tool to perform AWS and Azure security best practices assessments, audits, incident response, continuous monitoring, hardening and forensics readiness
-  [**AWS Consoler**](https://github.com/NetSPI/aws_consoler): A utility to convert your AWS CLI credentials into AWS console access
-  [**awsenum**](https://github.com/zer1t0/awsenum): awsenum is a tool to identify what permissions your account has in AWS by bruteforcing the different operations and check what can you perform. It is only limited to read operations
-  [**Enumerate IAM**](https://github.com/andresriancho/enumerate-iam): Tool to enumerate IAM permissions
-  **[Scout Suite](https://github.com/nccgroup/ScoutSuite)**: Scout Suite is an open source multi-cloud security-auditing tool, which enables security posture assessment of cloud environments
-  **[WeirdAAL](https://github.com/carnal0wnage/weirdAAL)**: AWS Attack Library
-  [**Hacktricks Cloud AWS Pentesting**](https://cloud.hacktricks.xyz/pentesting-cloud/aws-pentesting): Collection of AWS attack vectors and methodologies

```
git clone [https://github.com/carnal0wnage/weirdAAL.git](https://github.com/carnal0wnage/weirdAAL.git?ref=nomtechbytes.com)  
cd weirdAAL  
python3 -m venv weirdAAL  
source weirdAAL/bin/activate  
pip3 install -r requirements.txt
```

https://nomtechbytes.com/aws-iam-recon/

