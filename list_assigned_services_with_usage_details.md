### List assigned Services with usage details

Text

Command:
```
curl --header "Accept: application/json" http://user:password@127.0.0.1:8081/ecc/v1/subscriptions/46708421488/services
```

Request:
```
GET /ecc/v1/subscriptions/46708421488/services HTTP/1.1
Host: 127.0.0.1:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json 
```

Response:
```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 16:14:36 GMT
Content-Length: 334

{
  "msisdn" : "46708421488",
  "services" : [ {
    "name" : "Data1G",
    "value" : 88,
    "expires" : "Thu Mar 10 17:14:36 CET 2016"
  }, {
    "name" : "Data1G",
    "value" : 88,
    "expires" : "Thu Mar 10 17:14:36 CET 2016"
  }, {
    "name" : "Data5G",
    "value" : 88,
    "expires" : "Thu Mar 10 17:14:36 CET 2016"
  } ]
}
```