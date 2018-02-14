### Change Static IP

Change the static IP of a subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired static IP.

Note that this feature is only applicable for subscriptions that have been enabled for static IP support as part of the onboarding process.

Only valid IPv4 addresses are allowed.

**Example Command:**

```
curl --request PATCH \
 --data '{"static-ip" : "192.168.1.1}' \
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
  "static-ip" : "192.168.1.1"
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



