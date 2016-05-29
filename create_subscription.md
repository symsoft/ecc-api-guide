### Create a Subscription

A new Subscription is created by issuing a POST request on the _/ecc/v1/subscriptions_ path. The body of the request must include the _[iccid](parameters.md#iccid)_ to associate a SIM with the Subscription. Typically the _[msisdn](parameters.md#msisdn)_ is also needed unless it's a MSISDN less subscription. 

Once the Subscription is created it will be accessible via the _/ecc/v1/subscriptions/{type}:{id}_ path.

__Example Command:__
```
curl --header "Content-Type: application/json" \
 --header "Accept: application/json" \
 --data '{"msisdn": "46708421488", "iccid": "89461177710001700003"}' \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions
```

__Example Request:__
```
POST /ecc/v1/subscriptions HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 61

{
  "msisdn": "46708421488",
  "iccid": "89461177710001700003"
}
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```

