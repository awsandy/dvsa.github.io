---
title: "Install Kubernetes Tools"
chapter: false
weight: 28
---


## Install the tools required for the workshop

Clone the workshop repo and use a helper script to setup the workshop tools: 

```bash
cd ~/environment
```

```bash
rm -rf ecs-squid
git clone https://github.com/awsandy/ecs-squid.git
cd ~/environment/ecs-squid
```

Next run the setup script to install various tools we will use in the workshop, setup some environment variables, resize the root file system to 32GB and change the Cloud9 IDE to use the predefined `eksworkshop-admin` instance profile/role.

```bash
source scripts/setup.sh
```


Expected output will be similar to:

```
Install OS tools
Update OS tools
Existing lock /var/run/yum.pid: another copy is running as pid 10092.
Another app is currently holding the yum lock; waiting for it to exit...
  The other application is: yum
    Memory :  58 M RSS (306 MB VSZ)
    Started: Fri Jul  7 06:47:52 2023 - 00:01 ago
    State  : Running, pid: 10092
Another app is currently holding the yum lock; waiting for it to exit...
  The other application is: yum
    Memory : 256 M RSS (503 MB VSZ)
    Started: Fri Jul  7 06:47:52 2023 - 00:03 ago
    State  : Running, pid: 10092
Update pip
Uninstall AWS CLI v1
Install AWS CLI v2
AWS_REGION is eu-west-1
export ACCOUNT_ID=xxxxxxxx
export AWS_REGION=eu-west-1
export AZS=(eu-west-1a eu-west-1b eu-west-1c)
export TF_VAR_region=eu-west-1
eu-west-1
Check Cloud9 AWS Managed temporary credentials are disabled - in AWS Settings
ssh key
Setup Terraform cache
cp: cannot stat ‘./dot-terraform.rc’: No such file or directory
ssm cli add on
install tfsec ...
pip3
git-remote-codecommit
CHANGED: disk=/dev/nvme0n1 partition=1: start=4096 old: size=20967390,end=20971486 new: size=67104734,end=67108830
Filesystem     1M-blocks  Used Available Use% Mounted on
/dev/nvme0n1p1     32164  6715     25352  21% /
Verify ....
jq in path
aws in path
wget in path
terraform in path
Collecting awslogs
  Downloading https://files.pythonhosted.org/packages/28/ad/4cd970ce342cb38d475c6e02c09a241ffb35f77c0539549bb08a0852262d/awslogs-0.14.0-py2.py3-none-any.whl
Requirement already up-to-date: jmespath<1.0.0,>=0.7.1 in /usr/local/lib/python3.6/site-packages (from awslogs)
Collecting termcolor>=1.1.0 (from awslogs)
  Downloading https://files.pythonhosted.org/packages/8a/48/a76be51647d0eb9f10e2a4511bf3ffb8cc1e6b14e9e4fab46173aa79f981/termcolor-1.1.0.tar.gz
Requirement already up-to-date: python-dateutil>=2.4.0 in /usr/local/lib/python3.6/site-packages (from awslogs)
Collecting boto3>=1.5.0 (from awslogs)
  Downloading https://files.pythonhosted.org/packages/75/ca/d917b244919f1ebf96f7bbd5a00e4641f7e9191b0d070258f5dc10f5eaad/boto3-1.23.10-py3-none-any.whl (132kB)
    100% |████████████████████████████████| 133kB 7.0MB/s 
Requirement already up-to-date: six>=1.5 in /usr/local/lib/python3.6/site-packages (from python-dateutil>=2.4.0->awslogs)
Requirement already up-to-date: s3transfer<0.6.0,>=0.5.0 in /usr/local/lib/python3.6/site-packages (from boto3>=1.5.0->awslogs)
Requirement already up-to-date: botocore<1.27.0,>=1.26.10 in /usr/local/lib/python3.6/site-packages (from boto3>=1.5.0->awslogs)
Requirement already up-to-date: urllib3<1.27,>=1.25.4 in /usr/local/lib/python3.6/site-packages (from botocore<1.27.0,>=1.26.10->boto3>=1.5.0->awslogs)
Installing collected packages: termcolor, boto3, awslogs
  Running setup.py install for termcolor ... done
Successfully installed awslogs-0.14.0 boto3-1.23.10 termcolor-1.1.0
You are using pip version 9.0.3, however version 23.1.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
Enable bash_completion
bash: /home/ec2-user/.bash_completion: No such file or directory
PASSED: AWS_REGION is eu-west-1
PASSED: TF_VAR_region is eu-west-1
PASSED: ACCOUNT_ID is xxxxxxxxxxxx
bash: cd: /home/ec2-user/environment/tfekscode/lb2: No such file or directory
Associate eksworkshop-admin
{
    "IamInstanceProfileAssociation": {
        "AssociationId": "iip-assoc-0d839a7047a0a431f",
        "InstanceId": "i-0fcc60d545d4addfb",
        "IamInstanceProfile": {
            "Arn": "arn:aws:iam::xxxxxxxxxxxx:instance-profile/cloud9/eksworkshop-admin",
            "Id": "AIPAUSFNYOEGFBNZR63WM"
        },
        "State": "associating"
    }
}
removed ‘/home/ec2-user/.aws/credentials’
Profile eksworkshop-admin associated successfully.
For final checks - run scripts/check.sh
```


---

#### Check the Cloud9 IDE is setup correctly:

```bash
scripts/check.sh
```

Provided the Cloud9 workspace was setup as described the following script should show 3x `PASSED:` messages:

```
Checking workshop setup ...
PASSED: Cloud9 IDE name is valid 
PASSED: IAM role valid
PASSED: Found Instance profile eksworkshop-admin - proceed with the workshop
```

----

## [Next](./workspaceiam.md)



