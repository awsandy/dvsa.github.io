## Deploy the sample microserves app and explore observability

### Build the sample application with Terraform

```bash
cd ~/environment/ecs-squid/lab2/mesh-microservice-app/
```

```bash
terraform init
terraform plan -out tfplan
```

```bash
terraform apply tfplan
```


----

Monitor the ECS console and wait for all the services Last Deployment state to be indicated as  `completed`


Start a siege (worklaod)

get the load balancer DNS name

```bash
lbdns=$(aws ssm get-parameter --name /ecsworkshop/meshlb-dns --query Parameter.Value --output text)
echo $lbdns
```

Open a browser tab on that website address

And in a new terminal window start siege

```bash
siege -c 20 -i http://$lbdns
```


### Explore the observabilty of the deployed application:

[Using Container Insights](https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#container-insights:infrastructure/map){:target="_blank"}

[Using X-Ray](https://eu-west-1.console.aws.amazon.com/cloudwatch/home?region=eu-west-1#xray:service-map/map){:target="_blank"}


----

## [Next](./LAB-3.md)

