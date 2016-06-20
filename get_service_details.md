### Get Service details

Service details for a service identified by its _sid_ assigned to a Subscription can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}/services/{sid}_ path.

The response contains a representation of the Service with optionally an associated usage value and an expiry date. This would depend upon how the Service was defined during the [onboarding](onboarding.md) procedure.  

Note that it is possible that the same Service appears more than once. This will happen if the Service definition allows multiple instances of the Service and the Subscriber has been assigned multiple instances of the Service.

__Example Command:__
```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488/services/cfnr
```

__Example Request:__
```
GET /ecc/v1/subscriptions/msisdn:46708421488/services HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json 
```

__Example Response:__
```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 104

{
  "msisdn" : "46708421488",
  "services" : [ {
    "id" : "cfnr",
    "forward-number" : "46812312345",
  } ]
}
```