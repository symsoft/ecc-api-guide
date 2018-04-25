### Get Service details

Service details for a service identified by its _sid_ assigned to a Subscription can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}/services/{sid}_ path.

The response contains a representation of the Service which depends of the type of [services](services.md) and upon how the Service was defined during the [onboarding](onboarding.md) procedure.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/services/cfnr
```

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488/services/cfnr HTTP/1.1
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
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 104

{
    "id" : "cfnr",
    "forward-number" : "46812312345"
  } 
}
```

Note that it is possible that the same Service appears more than once. This will happen if the Service definition allows multiple instances of the Service and the Subscriber has been assigned multiple instances of the Service.

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488/services/Data1G HTTP/1.1
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
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 104

{
    "id : "Data1G"
    "instances" :
    [ {
    "instance" : "b78",
    "value" : 1000,
    "expires" : "Thu Mar 22 18:50:23 CET 2016"
  }, {
    "instance" : "a77",
    "value" : 556,
    "expires" : "Thu Mar 16 10:20:11 CET 2016"
  } ]
}
```



