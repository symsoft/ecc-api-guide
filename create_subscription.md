### Create a Subscription

Text and example goes here

POST on /ecc/v1/subscriptions

Command:
```
curl --header "Content-Type: application/json" --data @createReq.json http://user:password@172.16.20.14:8081/ecc/v1/subscribers
```
Where the _createReq.json_ file contains the body of the request.

Request:
```
POST /ecc/v1/subscribers HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: */*
Content-Type: application/json
Content-Length: 61
{
  "msisdn": "46708421488",
  "iccid": "89461177710001700003"
}
```

Response:
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```

__Note:__ In the current version of the API it is the responsibility of the User to allocate and keep track of MSISDNs. 