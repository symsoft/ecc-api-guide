### Withdraw a Service

__TODO:__ Text

Note that all instances of the service will be withdrawn.

__Example Command:__
```
curl --verbose -request DELETE --header "Accept: application/json" http://super:super@127.0.0.1:8081/ecc/v1/subscriptions/46708421488/services/Data5G
```

__Example Request:__
```
DELETE /ecc/v1/subscriptions/46708421488/services/Data5G HTTP/1.1

TODO
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```
