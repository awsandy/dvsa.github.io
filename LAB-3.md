
## Using CNCF Build packs

----

### Install the CNCF pack tool

```bash
(curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.29.0/pack-v0.29.0-linux.tgz" | sudo tar -C /usr/local/bin/ --no-same-owner -xzv pack)
```

### Use the paketo build pack:

```bash
pack config default-builder paketobuildpacks/builder:full
```

### Clone the demo:



```bash
pack build my-app --buildpack paketo-buildpacks/php \
  --builder paketobuildpacks/builder:full
```

```bash
docker run --interactive --tty --env PORT=8080 --publish 8080:8080 my-app
```

```bash
curl http://localhost:8080
```

or preview app in Cloud9

-----------

### Deploy the app to ECR

Push the docker image to ECR
Use terraform to create 
Add an ECS Task definition using the ECR image
Add an Service for this application 

```bash
cd ~/environment/ecs-squid/lab3/tf-app
```


Find the load balancer URL

```
lb-url=$(aws ssm get-parameter --name /ecsworkshop/proxy-dns --region eu-west-1 --query Parameter.Value --output text)

curl $lb-url:8080

```

-------


### Explore the other examples here:

cd ~environment/lab3/samples/tree/main/php

Repeat the above steps


-----




## Cleanup

```bash
cd ~/environment/ecs-squid/lab3/tf-example
terraform destroy -auto-approve
```

## [Next](./WRAPUP.md)





