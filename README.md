## Cleanup Commands

Remove all containers:

```
docker container rm -f $(docker container ls -aq)
```

Reclaim disk space:

```
docker image rm -f $(docker image ls -f reference='diamol/*' -q)
```


