### Change MSISDN

__TODO:__ Text and example goes here 

PATCH /ecc/v1/subscribers/NNNNNN with new [MSISDN](parameters.md#msisdn).

Once changed, the main URL for the Subscription changes.

__Example Command:__
```
curl TODO
```

__Example Request:__
```
PATCH /ecc/v1/subscriptions/46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: */*
Content-Type: application/json
Content-Length: 61

{
  "msisdn": "46705123456"
}
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```
