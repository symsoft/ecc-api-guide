### Set APN identifiers

Set the APN identifiers for a subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired APN identifiers. The given APN identifiers will replace the currently set APN identifiers.

The valid set of APN identifiers are defined as part of the onboarding process.

The first id in the `apn-ids` list will be used as the default APN identifier.

**Example Command:**

```
curl --request PATCH \
 --data '{"apn-ids" : [1, 2, 3]}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
PATCH /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 24

{
  "apn-ids" : [1, 2, 3]
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

### Get APN identifiers

The currently set APN identifiers of a subscription can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request will include a list of APN identifiers in the `apn` parameter.

The first APN identifier in the `apn` list is the default APN identifier.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: 172.16.20.14:8081
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
  "blocked" : false,
  "imsi": [
    "244141000170000"
  ],
  "apn" : [
    { "id" : 1, "name" : "internet" },
    { "id" : 2, "name" : "mms" },
    { "id" : 3, "name" : "voice" }
  ]
}
```



