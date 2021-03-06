### Get basic Subscription information

The basic information associated with a Subscription can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}_ path.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121

{
  "msisdn" : "46708421488",
  "iccid" : "89461177710001700003",
  "status" : "IN_USE",
  "blocked" : false,
  "imsi": [
    "244141000170000"
  ],
  "subscription-type" : "type one",
  "main-imsi" : "244141000170000",
  "odb-profile" : 1,
  "apn" : [],
  "tags" : [],
  "ongoing-orders" : []
}
```



