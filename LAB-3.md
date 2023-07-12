
## Using CNCF Build packs

----

### Install the CNCF pack tool

```bash
cd ~/environment/ecs-squid/lab3
(curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.29.0/pack-v0.29.0-linux.tgz" | sudo tar -C /usr/local/bin/ --no-same-owner -xzv pack)
```

### Use the paketo build pack:

```bash
pack config default-builder paketobuildpacks/builder:full
```

### Build a container using CNCF pack:

```
cd ~/environment/ecs-squid/lab3/samples/php/builtin-server
```


```bash
pack build my-app --buildpack paketo-buildpacks/php
```

List the local image `my-app` that has been created

```bash
docker image ls
```

run the image locally:


```bash
docker run --interactive --tty --env PORT=8080 --publish 8080:8080 my-app
```

----

From another terminal:

```bash
curl http://localhost:8080
```

Expected output similar to:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Powered By Paketo Buildpacks</title>
  </head>
  <body>
<img style="display: block; margin-left: auto; margin-right: auto; width: 50%;" src="https://paketo.io/images/paketo-logo-full-color.png"></img>  </body>
</html>
```


-----------


### Deploy the app to ECR

- Push the docker image to ECR
- Add an ECS Task definition using the ECR image
- Add an ECS Service for this application 


There is a Terraform sample to do this:

```bash
cd ~/environment/ecs-squid/lab3/tf-app
export TF_VAR_app_name=my-app
terraform init
terraform plan -out tfplan && terraform apply tfplan

```


Find the load balancer URL

```bash
lburl=$(aws ssm get-parameter --name /ecsworkshop/squid-lbdns --region eu-west-1 --query Parameter.Value --output text)
curl $lburl:8080
```

If the above doesn't work ? - check the new service has reached completed status in the `squid-ecr-ECSCluster` [ECS cluster](https://eu-west-1.console.aws.amazon.com/ecs/v2/clusters/squid-ecr-ECSCluster/services?region=eu-west-1){:target="_blank"}

![fleet](./static/images/my-app.png)

Verify connectivity with :

```bash
namp $lburl -Pn -p 8080 | grep open
```

This should show as part of the output:

PORT     STATE SERVICE

8080/tcp **open**  http-proxy

Retry the curl:

```bash
curl $lburl:8080
```

-------


### Optional - Explore the other examples here:

```bash
cd ~environment/lab3/samples/tree/main/php
```


Repeat the above steps


-----



## Cleanup

```bash
cd ~/environment/ecs-squid/lab3/tf-app
terraform destroy -auto-approve

```

---

## [Next](./WRAPUP.md)





