### Change SIM

The SIM associated with a Subscription can be changed by issuing a PATCH request on the _/ecc/v1/subscriptions/{msisdn}_ path. The body of the request must include the _[iccid](parameters.md#iccid)_ of the new SIM to be associated with the Subscription.

The old SIM is deleted and void after this operation.

__Note:__ The change of SIM card is performed more or less immediately. There is currently no API operation to perform a deferred SIM swap. 

__Example Command:__
```
curl --request PATCH \
--data '{"iccid": "89461177710001700011"}' \
--header "Content-type: application/json" \
--header "Accept: application/json" \
https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488
```

__Example Request:__
```
PATCH /ecc/v1/subscriptions/46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 61

{
  "iccid": "89461177710001700011" 
}
```


__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```

