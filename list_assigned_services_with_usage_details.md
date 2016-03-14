### List assigned Services with usage details

__TODO:__ Text

__Example Command:__
```
curl --header "Accept: application/json" https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488/services
```

__Example Request:__
```
GET /ecc/v1/subscriptions/46708421488/services HTTP/1.1
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
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 334

{
  "msisdn" : "46708421488",
  "services" : [ {
    "name" : "Data1G",
    "value" : 1000,
    "expires" : "Thu Mar 22 18:50:23 CET 2016"
  }, {
    "name" : "Data1G",
    "value" : 900,
    "expires" : "Thu Mar 16 10:20:11 CET 2016"
  }, {
    "name" : "Data5G",
    "value" : 2,
    "expires" : "Thu Mar 10 17:14:36 CET 2016"
  } ]
}
```