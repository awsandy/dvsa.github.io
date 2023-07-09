## Deploy the squid proxy on ECS


### Examine the Terraform files

```bash
cd ~/environment/ecs-squid/lab1/tf-squid
```

### Deploy the squid application

```bash
terraform init
terraform validate
terraform plan -out tfplan
terraform apply tfplan
```

### Use the AWS console to verify / explore the deployment

Using the console find and explore these resources

* [The ECS Clusters](https://eu-west-1.console.aws.amazon.com/ecs/v2/clusters)
* [ECS service](https://eu-west-1.console.aws.amazon.com/ecs/v2/clusters/squid-ecr-ECSCluster/services?region=eu-west-1)
* ECS tasks
* Task definitions
* Load Balancers

Note which task definition is deployed and which container image 

-------

### Setup a custom squid docker image


Examine the files in this directory

```bash
cd ~/environment/ecs-squid/lab1/squid-docker
```

including our own allow list `allowedlist.txt` which contains one entry:

```
aws.amazon.com
```

And the `Dockerfile` for building the custom container image.


----


The following script will then use these files to build a custom image for squid - using a CICD pipeline that has already been setup:


```bash
cd ~/environment/ecs-squid/lab1/scripts
./custom-squid.sh
```

Track the build in [code pipeline](https://eu-west-1.console.aws.amazon.com/codesuite/codepipeline/pipelines?region=eu-west-1) and 
[code build](https://eu-west-1.console.aws.amazon.com/codesuite/codebuild/projects?region=eu-west-1)

After the built completes:
Observe the [ECR repo](https://eu-west-1.console.aws.amazon.com/ecr/repositories?region=eu-west-1) for the new custom squid image


-------

## Adjust Terraform to deploy our custom squid container

### Check the ECR repo for the custom squid image

```bash
cd ~/environment/ecs-squid/lab1/tf-squid
```

Observe the difference in these two files definition of which image to use:

```bash
grep task_definition aws_ecs_service__squid-ecr-ECSService.tf
```

```bash
grep task_definition aws_ecs_service__squid-ecr-ECSService.tf.custom
```

and the corresponding different images in the task definitions

```bash
grep image aws_ecs_task_definition__squip--standard-ecr-ECSTaskDefinition.tf
```

image = "public.ecr.aws/ubuntu/**squid**:latest"

```bash
grep image aws_ecs_task_definition__squid--custom-ecr-ECSTaskDefinition.tf
```

image = format("%s.dkr.ecr.%s.amazonaws.com/**squid-ecr-ecrrepository**:latest", data.aws_caller_identity.current.account_id, data.aws_region.current.name)


Next copy the custom service definition into place:

```bash 
cp aws_ecs_service__squid-ecr-ECSService.tf.custom aws_ecs_service__squid-ecr-ECSService.tf
```

Confirm the change being made with terraform plan

```bash
terraform plan -out tfplan
```

Apply the change:

```bash
terraform apply tfplan
```

-------


## Deploy a test instance


```bash
cd ~/environment/ecs-squid/lab1/test-instance
```

```bash
terraform init
terraform validate
terraform plan -out tfplan
terraform apply tfplan
```

----------

From your Cloud9 IDE terminal get and save the VPC endpoint DNS entry:

```bash
aws ssm get-parameter --name /ecsworkshop/proxy-dns --query Parameter.Value --output text
```

Connect to the instance via [SSM Fleet](https://eu-west-1.console.aws.amazon.com/systems-manager/managed-instances?region=eu-west-1){:target="_blank"}

Select the instance "test-squid"
Use the option, `Node action` then `Start terminal session`

From the OS prompt:

```bash
proxyurl=<the value you saved form the Cloud9 IDE>
export http_proxy=http://${proxyurl}:3128
export https_proxy=http://${proxyurl}:3128
```


### this works:

```bash
curl https://aws.amazon.com
```

### this does not:

```bash
curl https://www.microsoft.com
```

-------


## Cleanup


```bash
cd ~/environment/ecs-squid/lab1/test-instance
terraform destroy -auto-approve
```









