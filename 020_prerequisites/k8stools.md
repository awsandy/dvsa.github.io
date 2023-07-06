---
title: "Install Kubernetes Tools"
chapter: false
weight: 28
---

Amazon EKS clusters require - kubectl, the aws-cli or aws-iam-authenticator
binary to allow IAM authentication for your Kubernetes cluster.



#### Install the tools

Clone the workshop repo and use a helper script to setup the workshop tools: 

```bash
cd ~/environment
```

```bash
rm -rf ecs-squid
git clone 
```

#### Setup the workshop tools:

```bash
cd ~/environment/tfekscode
```

```bash
source setup
```

Check you see messages at the end of the output that terraform, kubectl, jq and aws in the path. Also that the AWS_REGION is set and the ACCOUNT_ID to a 12 digit number.


::::alert{type="success" header="Expected Output"}
:::code{showCopyAction=true showLineNumbers=false language=java}

Install OS tools
Install OS tools
Update OS tools
Update pip
Uninstall AWS CLI v1
Install AWS CLI v2
AWS_REGION is aa-west-x
export ACCOUNT_ID=xxxxxxxxxxxx
export AWS_REGION=aa-west-x
export TF_VAR_region=aa-west-x
eu-west-3
Setup Terraform cache
Setup kubectl
Install kubectl
install eksctl
eksctl completion
helm
add helm repos
"eks" has been added to your repositories
kubectx
ssh key
ssm cli add on
install tfsec ...
pip3
git-remote-codecommit
CHANGED: partition=1 start=4096 old: size=20967391 end=20971487 new: size=67104735 end=67108831
Filesystem     1M-blocks  Used Available Use% Mounted on
/dev/nvme0n1p1     32756  8656     24101  27% /
Verify ....
jq in path
aws in path
wget in path
kubectl in path
terraform in path
eksctl in path
helm in path
kubectx in path
Enable bash_completion
PASSED: AWS_REGION is aa-west-x
PASSED: TF_VAR_region is aa-west-x
PASSED: ACCOUNT_ID is xxxxxxxxxxxx
:::
::::


---

#### Check the Cloud9 IDE is setup correctly:

```bash
./check
```

Provided the Cloud9 workspace was setup as described the following script should show 3x `PASSED:` messages:

::::alert{type="success" header="Expected Output"}
:::code{showCopyAction=true showLineNumbers=false language=java}
Checking workshop setup ...
PASSED: Cloud9 IDE name is valid - contains eks-terraform
PASSED: IAM role valid - eksworkshop-admin
PASSED: Found Instance profile eksworkshop-admin - proceed with the workshop
:::
::::

----

Proceed to the next step

