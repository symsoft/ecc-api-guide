### Batches

Batches are a ECC feature that provides the possibility to send multiple API requests in a single HTTP request.

A batch can contain a maximum of 100 API requests.

When a batch is created it will be given an unique _batch id_ which later can be used to query the status of the batch.

A batch can have one of the following statuses:

| Status | Description |
| --- | --- |
| INITIALISING | The batch and the contained API requests are being verified |
| PROCESSING | API requests are being processed |
| COMPLETED | Orders for all API requests have completed successfully |
| PARTIALLY\_COMPLETED | All API requests have been executed, but at least one API request completed with status REJECTED, FAILED or CANCELED. |

When a batch is completed, or partially completed, an event will be generated which can be retrieved via the [events](events.md) resource.

Note that an individual API request, contained in the batch, will also generate an _order complete_ event when the corresponding order has completed. This _order complete_ event will contain the _batch id_ corresponding to the batch that contained the API request.

A batch may be of type:

* _single_ - executes API requests in parallell. This is the default if no type is specified.
* _multi_ -  executes API requests sequentially _per subscription_ \(grouped by _iccid_\) in the order they appear in the batch. This can be useful when performing operations that are logically connected on a specific subscription. For example creating a subscription and adding services. All requests in a _multi_ batch must specify an _iccid_.

Each API request contained in a batch can have one of the following statuses:

| Status | Description |
| --- | --- |
| APPROVED | API request is approved, but no order has been created yet |
| REJECTED | API request is rejected. e.g due to formatting error |
| FAILED | No order could be created for the request, e.g. due to that the subscription was not found |
| PROCESSING | An order has been created and provisioning is ongoing |
| COMPLETED | The order has successfully completed |
| CANCELED | The order execution failed, contact support for more information. |

Batches will be automatically removed after 60 days.

#### Submit a batch

A new Batch is created by issuing a POST request on the _/ecc/v1/batches_ path. The _requests_ parameter shall contain an array of API requests that will be executed. Each API request may also, optionally, contain a _requestid_ parameter carrying an identifier for the specific API request. This identifier can be used by the ECC API user to correlate API requests when retrieving information about a batch, see [Get information about a batch](#get-information-about-a-batch)

The following API requests are supported in a Batch request:

| API request | Method | Resource |
| --- | --- | --- |
| Create subscription | POST | subscriptions |
| Block/Unblock subscription | PATCH | subscriptions/{type}:{id} |
| Change state of a subscription | PATCH | subscriptions/{type}:{id} |
| Assign a service | POST | subscriptions/{type}:{id}/services |
| Withdraw a service | DELETE | subscriptions/{type}:{id}/services |
| Modify a service | PATCH | subscriptions/{type}:{id}/services |

If the batch is of type _multi_, the requests will be handled sequentially _per subscription_ \(grouped by _iccid_\) in the order they appear in the list. This means that a subsequent request will not be handled until all earlier requests for a subscription have successfully completed. If one request completes with status CANCELED the execution of the requests for this subscription is stopped. The requests that have not been executed will have status APPROVED.

**Example of type **_**single**_** Request:**

```
POST /ecc/v1/batches HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: XXX

{
    "type": "single",
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

**Example Response:**

```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: XXX

{
  "batchid": "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
  "creationdate": "2017-01-01T12:00:27.87+00:20"
  "status": "INITIALIZING",
  "requests": [
      {
        "requestid": "127322",
        "status": "APPROVED",
        "info": null,
        "orderid": null
      },
      {
        "requestid": "127323",
        "status": "APPROVED",
        "info": null,
        "orderid": null
      },
      {
        "requestid": "127324",
        "status": "APPROVED",
        "info": null,
        "orderid": null
      },
      {
        "requestid": "127325",
        "status": "REJECTED",
        "info": "Missing id parameter in body",
        "orderid": null
      }
  ]
}
```

#### Get information about a batch

Information about a previously submitted batch can be retrieved by issuing a GET request on the _/ecc/v1/batches/{batchid}_ path.

The response contains information about the batch as well as information about each individual API request in the batch.

The _status_ parameter for the batch indicates the status of the batch.

Please note that if a provisioning order fails the request status will still be PROCESSING. The status of an order can be checked by issuing a request using the [orders](orders.md) end-point with the order id corresponding to the request. Provisioning failures requires manual intervention in order to resolve.

**Example Request:**

```
GET /ecc/v1/batches/f81d4fae-7dec-11d0-a765-00a0c91e6bf6 HTTP/1.1
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
Content-Length: XXX

{
  "batchid": "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
  "creationdate": "2017-01-01T12:00:27.87+00:20"
  "status": "PROCESSING",
  "requests": [
      {
        "requestid": "127322",
        "orderid": 23901,
        "status": "PROCESSING",
        "info": null
      },
      {
        "requestid": "127323",
        "orderid": 23902,
        "status": "COMPLETED",
        "info": null
      },
      {
        "requestid": "127324",
        "orderid": null,
        "status": "FAILED",
        "info": "Subscription not found"
      },
      {
        "requestid": "127325",
        "orderid": null,
        "status": "REJECTED",
        "info": "Missing id parameter in body"
      }
  ]
}
```



