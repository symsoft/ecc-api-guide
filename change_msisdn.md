### Change MSISDN

The [_msisdn_](parameters.md#msisdn) associated with a Subscription can be changed by issuing a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}}_ path. \(If the type is "msisdn" the id is the old msisdn\) The body of the request must include the new [_msisdn_](parameters.md#msisdn) to be associated with the Subscription.

Once the change is executed the Subscription will be accessible via the _/ecc/v1/subscriptions/msisdn;{new msisdn}_ path, i.e. the main path for the Subscription changes.

**Example Command:**

```
curl --request PATCH \
 --data '{"msisdn" : "46705123456"}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/46708421488
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
  "msisdn": "46705123456"
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



