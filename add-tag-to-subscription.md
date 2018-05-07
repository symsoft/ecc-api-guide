### Add Tag on Subscription

A tag is added on a subscription by issuing a POST request on the _/ecc/v1/subscriptions/{type}:{id}_/tags/_{tag}_ path.

See [Tags](/tags.md) for further information about tags.

**Example Command:**

```
curl --request POST \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/tags/customer_1234
```

**Example Request:**

```
POST /ecc/v1/subscriptions/msisdn:46708421488/tags/customer_1234 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
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



