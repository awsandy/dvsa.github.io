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

* [The ECS Clusters](https://eu-west-2.console.aws.amazon.com/ecs/v2/clusters)
* ECS service
* ECS tasks
* Task definitions
* Load Balancers

Note which task definition is deployed and which container image 

-------

### Setup a custom squid docker image

```bash
squid/setup-custom-squid.sh
```

Track the build in code pipeline / build

Observe the ECR repo


-------

## Adjust Terraform to deploy our squid container

### Check the ECR repo for the custom squid image

```bash
cd cd ~/environment/ecs-squid/tf-squid
```

edit the file:    `aws_ecs_service__squid-ecr-ECSCluster__squid-ecr-ECSService.tf`

Change this line:

`task_definition       = aws_ecs_task_definition.squid--standard-ecr-ECSTaskDefinition.arn`

to:

`task_definition       = aws_ecs_task_definition.squid--custom-ecr-ECSTaskDefinition.arn`


**save your changes !**

Confirm the change being made with terraform plan

```bash
terraform plan -out tfplan
```

Apply the change:

```
terraform apply tfplan
```

-------


Next deploy a test instance

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


Connect to the insytance via [SSM Fleet](https://eu-west-2.console.aws.amazon.com/systems-manager/managed-instances?region=eu-west-2)

From the OS prompt:

```bash
proxyurl=$(aws ssm get-parameter --name /ecsworkshop/proxy-dns --region eu-west-2 --query Parameter.Value --output text)
export http_proxy=http://${proxyurl}:3128
export https_proxy=http://${proxyurl}:3128
```


### this works
```bash
curl https://aws.amazon.com
```

### this does not

```bash
curl https://www.microsoft.com
```



-------

## Cleanup

```bash
cd ~/environment/ecs-squid/lab1/test-instance
terraform destroy -auto-approve
```









