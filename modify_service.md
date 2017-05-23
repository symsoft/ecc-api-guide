### Modify Service

Some service attributes, such as _forward-number_ for supplementary-service and _limit_ for reccuring-bucket can be changed by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}/services/{sid}_ path. The body of the request shall include the attribute to change.

**Example Command:**

```
curl --request PATCH \
 --data '{"forward-number" : "467012312345"}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488/subscriptions/cfnr
```

**Example Request:**

```
PATCH /ecc/v1/subscriptions/msisdn:46708421488/services/cfnr HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 61

{
  "forward-number" : "467012312345"
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



