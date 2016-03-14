### Delete a Subscription

A Subscription can be deleted by issuing a DELETE request on the _/ecc/v1/subscriptions/{msisdn}_ path. 

The associated SIM is deleted and void after this operation.


__Example Command:__
```
curl --request DELETE \
 --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/46708421488
```

__Example Request:__
```
DELETE /ecc/v1/subscriptions/46708421488 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```

---
__TODO:__ Must decide and describe if a SIM is dead (deleted) after this operation. In a future version we may have multiple Subscription Types. It may be so that a change of Subscription Type only can be performed by means of a delete & create, and is such case the SIM is to be re-used. For a normal deletion the SIM should be dead and not used ever again. 

