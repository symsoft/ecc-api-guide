### Assign a Service

__TODO:__ Text

Note that if the service allows multiple instances then multiple invocations of the same command will result in multiple instances of the service.

__Example Command:__
```
curl --request POST --header "Accept: application/json" https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488/services/Data5G
```

__Example Request:__
```
POST /ecc/v1/subscriptions/46708421488/services/Data5G HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Mon, 14 Mar 2016 12:18:50 GMT
Content-Length: 0
```

---
__TODO:__ Is it wise (stringent) to POST without body?