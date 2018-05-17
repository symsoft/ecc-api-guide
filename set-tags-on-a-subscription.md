### Replace Tags on Subscription

The currently set tags on a subscription can be replaced by issuing a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the complete set of tags that should be applied to the subscription.

This is similar to [Add Tag on Subscription](/add-tag-to-subscription.md) and [Remove Tag from Subscription](/remove-tag-from-subscription.md), but this operation replaces the currently set tags on the subscription with the tags in this request.

See [Tags](/tags.md) for further information about tags.

**Example Command:**

```
curl --request PATCH \
 --data '{"tags" : [ "customer_1234", "country_se" ]}' \
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
Content-Type: application/json
Accept: application/json
Content-Length: 44

{"tags" : [ "customer_1234", "country_se" ]}
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



