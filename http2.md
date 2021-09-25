## Check if HTTP2 is Used

```
curl -vso /dev/null --http2 https://www.codingskill.net
```

Look for:

```
* Using HTTP2, server supports multi-use
* Connection state changed (HTTP/2 confirmed)
```

