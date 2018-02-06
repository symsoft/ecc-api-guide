### Change A2P Voice Application Key

Change the A2P Voice Application Key  assigned to the  Subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired application key. Note that this feature is only applicable for subscriptions that have been enabled for A2P Voice support as part of the onboarding process.  
This property can also be supplied when creating a subscription.

**Example Command:**

```
curl --request PATCH \
 --data '{"a2p-voice-app-key" : "appkey"}' \
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
Content-Length: 43

{
  "a2p-voice-app-key" : "appkey"
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



