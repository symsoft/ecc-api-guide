### Change Static IP Address

Change the static IP address of a subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired static IP address.

Note that this feature is only applicable for subscriptions using an APN with static IP enabled. It will not affect the IP address of a susbcription using an APN with dynamic allocation of IP addresses.

Only valid IPv4 addresses are allowed.

**Example Command:**

```
curl --request PATCH \
 --data '{"static-ip" : "192.168.1.1}' \
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



