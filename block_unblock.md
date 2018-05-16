### Block - Unblock

The blocking state a Subscription can be changed by issuing a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request must include the desired blocking state.

**Example Command:**

```
curl --request PATCH \
 --data '{"blocked": true}' \
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
  "blocked": true
}
```

**Example Response:**

```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 26
{
  "orders": [
    20144
  ]
}
```



