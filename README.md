## Connecting to a Container

```
docker container run -it diamol/base
```

Get details of all running containers:

```
docker container ls
```

List the process running in the container:

```
docker container top <container-id>
```

## Cleanup Commands

Remove all containers:

```
docker container rm -f $(docker container ls -aq)
```

Reclaim disk space:

```
docker image rm -f $(docker image ls -f reference='diamol/*' -q)
```

## Run a Website in a Container

```
docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web
```

View CPU, memory, network and disk usuage:

```
docker container stats <image-id-from-pervious-command>
```

## Use an Existing Image

Pull the image:

```
docker image pull diamol/ch03-web-ping
```

Run a container:

```
docker container run -d --name web-ping diamol/ch03-web-ping
```

## View the Logs

```
docker container logs web-ping
```

## Overriding Environment Variables

Use environment variable:

```
docker container run --env TARGET=google.com diamol/ch03-web-ping
```

## Disk Space Usage

```
docker system df
```

## Build an Image

From the project root folder, run:

```
docker image build --tag web-ping .
```

## View Images

```
docker image ls
```

Images starting with w:

```
docker image ls 'w*'
```

Configuration settings can be applied with environment variables:

```
docker container run -e TARGET=docker.com -e INTERVAL=5000 web-ping
```

## Check History of Image

```
docker image history web-ping
```

## Tag an Image

```
docker image build -t web-ping:v2 .
```

## Optimizing Dockerfile

Order instructions based on the change frequency. Instructions that are unlikely to change are at the start of the Dockerfile.

```
FROM diamol/node

CMD ["node", "/web-ping/app.js"]

ENV TARGET="blog.sixeyed.com" \
    METHOD="HEAD" \
    INTERVAL="3000" 

WORKDIR /web-ping
COPY app.js .
```

Rebuild the optimized image:

```
docker image build -t web-ping:v3 .
```







