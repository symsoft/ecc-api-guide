### Change MSISDN

The _[msisdn](parameters.md#msisdn)_ associated with a Subscription can be changed by issuing a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}}_ path. (If the type is "msisdn" the id is the old msisdn) The body of the request must include the new _[msisdn](parameters.md#msisdn)_ to be associated with the Subscription. 

Once the change is executed the Subscription will be accessible via the _/ecc/v1/subscriptions/msisdn;{new msisdn}_ path, i.e. the main path for the Subscription changes.

__Example Command:__
```
curl --request PATCH \
 --data '{"msisdn" : "46705123456"}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488
```

__Example Request:__
```
PATCH /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
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
Content-Length: 26

{
  "orders": [
    20144
  ]
}

```
