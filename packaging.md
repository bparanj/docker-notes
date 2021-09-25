## Create a Docker Network

```
docker network create nat
```

Run a container and connect to the nat network:

```
docker container run --name iotd -d -p 800:80 --network nat image-of-the-day
```

Run the second container and connect to the nat network:

```
docker container run --name accesslog -d -p 801:80 --network nat access-log
```

Run the third container and connect to the nat network:

```
docker image build -t image-gallery .
```

Run the go web application that consumes the API of other micro services:

```
docker container run -d -p 802:80 --network nat image-gallery
```

