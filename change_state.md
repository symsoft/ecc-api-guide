### Change State

Change the state of a Subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired state. States can be **BEFORE_FIRST_USE** or **IN_USE**. Please find definition of states below:

- **BEFORE_FIRST_USE**: Initial state of a Subscription. When state has been changed, it can never go back to **BEFORE_FIRST_USE**
- **IN_USE**: The state where the Subscriptionu se services,


__Example Command:__
```
curl --request PATCH \
 --data '{"state" : "IN_USE"}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488
```

__Example Request:__
```
PATCH /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 61

{
  "state" : "IN_USE"
}
```

__Example Response:__
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
