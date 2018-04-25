### Delete a Subscription

A Subscription can be deleted by issuing a DELETE request on the _/ecc/v1/subscriptions/{type}:{id}_ path.

The associated SIM is deleted and void after this operation.

**Example Command:**

```
curl --request DELETE \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
DELETE /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
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



