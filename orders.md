### Orders

Provisioning operations in the ECC API follow an asynchronous design. For the asynchronous operations the ECC API returns 202, Accepted and an orderId.

The ECC API only allows for one outstanding order per subscription and returns 409, Conflict if there is an outstanding order for a subscription.

The Order resource provides an API to retreive status about these orders.

The status for a specific provisioning operation can be checked by issuing a GET request on the _/ecc/v1/orders/{orderid}_ path.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/orders/10091
```

**Example Request:**

```
GET /ecc/v1/orders/10091 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 102

{
  "orderId": 20144,
  "msisdn" : "4612312312",
  "iccid" : "89461177710001700003",
  "status": "COMPLETED",
  "orderDate": "2016-03-10T00:00:00Z",
  "completionDate": "2016-03-10T00:00:05Z"
}
```

#### Orders statuses

A provisioning order may have one of the following statuses:

| Status | Description |
| :--- | :--- |
| COMPLETED | The order executed successfully |
| PROVISIONING | Provisioning is ongoing |
| CANCELED | The order execution was canceled, please contact support for more information |



