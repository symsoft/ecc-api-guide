### Payload

The Payload in API requests and responses is JSON, JavaScript Object Notation as specified in [ECMA-404](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf). This means that content declaring HTTP headers should be set accordingly.

**Example request header:**

```
POST /ecc/v1/subscriptions HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json                 <-- HERE
Content-Type: application/json           <-- HERE
Content-Length: 61

... body omitted ...
```



