### Change SIM

The SIM associated with a Subscription can be changed by issuing a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request must include the [_iccid_](parameters.md#iccid) of the new SIM to be associated with the Subscription.

The old SIM is deleted and void after this operation.

**Example Command:**

```
curl --request PATCH \
 --data '{"iccid": "89461177710001700011"}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
PATCH /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 61

{
  "iccid": "89461177710001700011" 
}
```

**Example Response:**

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



