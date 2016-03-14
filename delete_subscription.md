### Delete a Subscription

__TODO:__ Some text.

__Example Command:__
```
curl TODO
```

__Example Request:__
```
DELETE /ecc/v1/subscriptions/46708421488 HTTP/1.1

TODO
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 0
```

---
__TODO: Must decide and describe if a SIM is dead (deleted) after this operation. In a future version we may have multiple Subscription Types. It may be so that a change of Subscription Type only can be performed by means of a delete & create, and is such case the SIM is to be re-used. For a normal deletion the SIM should be dead and not used ever again.__ 

