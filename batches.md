### Batches
Batches are a ECC feature that provides the possibility to send multiple API requests in a single HTTP request.

#### Submit a batch
A new Batch is created by issuing a POST request on the _/ecc/v1/batches_ path. The body of the request shall contain an
array of API requests that will be executed.

The following API requests are supported in a Batch request:

| API request | Method | Path
|------------|--------| --------|
| Create subscription | POST | /ecc/v1/subscriptions |
| Block/Unblock subscription | PATCH | /ecc/v1/subscriptions/{type}:{id} |
| Assign services | PATCH | /ecc/v1/subscriptions/{type}:{id}/services |

__Example Request:__
```
POST /ecc/v1/batches HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: XXX

[
  {
    "method": "POST",
    "path": "/ecc/v1/subscriptions",
    "body": {
      "msisdn": "46708421499",
      "iccid": "89461177710001700003"
    }
  },
  {
    "method": "PATCH",
    "path": "/ecc/v1/subscriptions/msisdn:46708421488",
    "body": {
       "blocked": true
    }
  },
  {
    "method": "POST",
    "path": "/ecc/v1/subscriptions/msisdn:46708421477/services",
    "body": {
       "id": "data1GB",
       "limit": 100
    }
  }
]
```

__Example Response:__
```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: XXX

{
  "batchid": "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
  "creationdate": "2017-01-01T12:00:27.87+00:20"
  "status": "PENDING",
  {
    "orderid": null,
    "status": "SUBMIT_PENDING"
  },
  {
    "orderid": null,
    "status": "SUBMIT_PENDING"
  },
  {
    "orderid": null,
    "status": "SUBMIT_PENDING"
  }
}

```