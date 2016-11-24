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
  * Submitted timestamp
  * Total number of API calls with state=Completed
  * Duration from start to latest Completed API call
  * List of API calls

The list of API calls is an ordered list where each entry will started in the same order as in the list. Batch adds meta data to each API call:
* orderId
* Status [Not Submitted, Submitted, Completed]
* statusChangedTS : timestamp for latest status change

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
A new Batch is created by issuing a POST request on the _/ecc/v1/batches_ path. The _requests_ parameter shall contain an
array of API requests that will be executed.

The following API requests are supported in a Batch request:

| API request | Method | Resource
|------------|--------| --------|
| Create subscription | POST | subscriptions |
| Block/Unblock subscription | PATCH | subscriptions/{type}:{id} |
| Change state of a subscription | PATCH | subscriptions/{type}:{id} |
| Assign a service | POST | subscriptions/{type}:{id}/services |
| Withdraw a service | DELETE | subscriptions/{type}:{id}/services |
| Modify a service | PATCH | subscriptions/{type}:{id}/services |

If the batch contains multiple requests affecting the same subscription, these requests will be handled sequentially in the
order they appear in the list. This means that a subsequent request will not be handled until all earlier requests in the list, for the same
 subscription, have successfully completed.

__Example Request:__
```
POST /ecc/v1/batches HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: XXX

{
    "requests": [
      {
        "method": "POST",
        "resource": "subscriptions",
        "body": {
          "msisdn": "46708421499",
          "iccid": "89461177710001700003"
        },
        "requestid": "127322"
      },
      {
        "method": "PATCH",
        "resource": "subscriptions/msisdn:46708421488",
        "body": {
           "blocked": true
        },
        "requestid": "127323"
      },
      {
        "method": "POST",
        "resource": "subscriptions/msisdn:46708421466/services",
        "body": {
           "id": "Data1G",
           "limit": "100"
        },
        "requestid": "127324"
      },
      {
        "method": "POST",
        "resource": "subscriptions/msisdn:46708421477/services",
        "body": {
           "limit": 100
        },
        "requestid": "127325"
      }
    ]
}
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
  "status": "INITIALIZING",
  {
    "requestid": "127322",
    "status": "APPROVED"
  },
  {
    "requestid": "127323",
    "status": "APPROVED"
  },
  {
    "requestid": "127324",
    "status": "APPROVED"
  },
  {
    "requestid": "127325",
    "status": "REJECTED",
    "info": "Missing id parameter in body"
  }
}

```

#### Get information about a batch
Information about a previously submitted batch can be retrieved by issuing a GET request on the _/ecc/v1/batches/{batchid}_ path.

The response contains information about the batch as well as information about each individual request in the batch.

The _status_ parameter for the batch indicates the status of the batch. The following values are possible:

| Status value | Description |
| ---------- | ----------- |
| INITIALISING | The batch and the contained requests are being verified |
| PROCESSING | Requests are being processed |
| COMPLETED | Orders for all requests have completed |
| PARTIAL_COMPLETED | Orders for all valid requests have completed, but there exist some requests that have status REJECTED or FAILED |

For each valid request in the batch an order will be created and the corresponding order id will be given for the request.
Each request will also have a status and the following values are possible:

| Status value | Description |
| ---------- | ----------- |
| APPROVED | Request is approved, but no order has been created yet |
| REJECTED | Request is rejected. e.g due to formatting error |
| FAILED | No order could be created for the request, e.g. due to that the subscription was not found |
| PROCESSING | An order has been created and provisioning is ongoing |
| COMPLETED | The order has successfully completed |

Please note that if provisioning fails the request status will still be PROCESSING. The status of an order can be
checked by issuing a request using the order end-point with the order id corresponding to the request. Provisioning failures
 requires manual intervention in order to resolve.

__Example Request:__
```
GET /ecc/v1/batches/f81d4fae-7dec-11d0-a765-00a0c91e6bf6 HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: XXX

{
  "batchid": "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
  "creationdate": "2017-01-01T12:00:27.87+00:20"
  "status": "PROCESSING",
  "requests": [
      {
        "requestid": "127322",
        "orderid": 23901,
        "status": "PROCESSING"
      },
      {
        "requestid": "127323",
        "orderid": 23902,
        "status": "COMPLETED"
        "completiondate": "2017-01-01T12:00:37.87+00:20"
      },
      {
        "requestid": "127323",
        "status": "FAILED",
        "info": "Subscription not found"
      },
      {
        "requestid": "127325",
        "status": "REJECTED",
        "info": "Missing id parameter in body"
      }
  ]
}

```