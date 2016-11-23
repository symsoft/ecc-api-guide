### Batches
Batches are a ECC feature that provides the possibility to send multiple API requests in a single HTTP request.

Examples of situations when you might want to use batching:
  * Block multiple subscriptions in one request
  * Remove and add services for a subscription(s) in one and the same request

In each case, instead of sending each call separately, you can group them together into a single HTTP request. You can even group requests for multiple subscriptions.

You are limited to 100 calls in a single batch request. If you need to make more calls than that, use multiple batch requests.

It introduces a new Batches resource that provides an API to create and get status of a batch resource. A batch resource has the following properties:
  * Id
  * Status [Submitted, Completed]
  * Create timestamp
  * Total number of API calls with state=Completed
  * Duration from start to latest Completed API call
  * List of API calls

The list of API calls is an ordered list where each entry will started in the same order as in the list.

The life-cycle of a batch is simple:
  1.Create a batch with POST .../batches with list of API calls in the body.
  2. ECC API responds with 202 Accepted, the batch resource properties and the API call list where two fields have been added to each call:
    * orderId: see Order chapter. "orderId": will have -1 in the response to POST, because the order has not yet been created yet.
    * Status: Not Submitted

  3. Get batch status with GET /batches/batchId:17
  4. ECC API responds with 200 OK, the batch properties and the API call list with updates orderId and status [Not Submitted, Submitted, Completed]
  5. When the batch is completed, all API Calls have status Completed, then ECC API notifies the client with Batch completed event that contains the batchId.
  6. The batch job will be stored for 60 days and will then be deleted.

Note that the ECC API will generate an order-completed event per API call in the batch and these events contains both the OrderId and the BatchId.

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
