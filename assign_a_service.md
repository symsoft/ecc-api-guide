### Assign Services

Services can be assigned to a Subscription by issuing a POST request on the _/ecc/v1/subscriptions/{type}:{id}/services_ path.   
The body of the request includes the different services.

**Example Command:**

```
curl --request POST \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/services/
```

**Example Request:**

```
POST /ecc/v1/subscriptions/msisdn:46708421488/services HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 101

{
  "services": [
    {
      "id": "data1GB",
      "limit": 100
    },
    {
      "id": "cfu",
      "forward-number":"467012312334" 
    }
  ]
}
```

**Example Response:**

```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Mon, 14 Mar 2016 12:18:50 GMT
Content-Length: 26
{
  "orders": [
    20144
  ]
}
```

Bucket services types allows multiple instances so a new ‘instances’ are created each time this type of service is assigned to a subscription.

