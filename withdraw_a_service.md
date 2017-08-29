### Withdraw a Service

A Service can be withdrawn from a Subscription by issuing a DELETE request on the _/ecc/v1/subscriptions/{type}:{id}/services/{sid}_ path.

**Note** If the service is of the _**bucket**_ type all instances of the service will be withdrawn. To remove a specific instance of a bucket type service the [Withraw a Service instance ](withdraw_a_specific_service_instance.md) should be used.

**Example Command:**

```
curl -request DELETE \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488/services/Data5G
```

**Example Request:**

```
DELETE /ecc/v1/subscriptions/msisdn:46708421488/services/Data5G HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Mon, 14 Mar 2016 12:23:37 GMT
Content-Length: 26

{
  "orders": [
    20144
  ]
}
```



