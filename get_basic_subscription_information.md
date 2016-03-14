### Get basic Subscription information

__TODO:__ Text and example here.

__Example Command:__
```
curl --verbose --header "Accept: application/json" http://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488
```

__Example Request:__
```
GET /ecc/v1/subscriptions/46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 87

{
  "msisdn" : "46708421488",
  "iccid" : "89461177710001700003",
  "blocked" : false
}
```