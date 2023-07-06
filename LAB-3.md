
## Using CNCF Build packs

----

### Install the CNCF pack tool

```bash
(curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.29.0/pack-v0.29.0-linux.tgz" | sudo tar -C /usr/local/bin/ --no-same-owner -xzv pack)
```

### Clone the demo:

```bash
git clone https://github.com/paketo-buildpacks/samples
cd samples/php/builtin-server
```

```bash
pack build my-app --buildpack paketo-buildpacks/php \
  --builder paketobuildpacks/builder:full
```

```bash
docker run --interactive --tty --env PORT=8080 --publish 8080:8080 php-builtin-server-sample
```

```bash
curl http://localhost:8080
```

or preview app in Cloud9

-----------

### Deploy the app to ECR

Push the docker image to ECR

Use terraform to create 

An ECS Task definition using the ECR image
An Service for this application 


-------


### Explore the other examples here:

cd ~environment/lab3/samples/tree/main/php

Repeat the above steps


-----

## [Next](./WRAPUP.md)





