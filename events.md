### Events

Events are a ECC feature that provides comprehensive event-logging for ECC Subscription.

A number of events are supported, for example, when a usage threshold is passed, state change, mobile network change, device change, and so on.

The Events resource provides an API to retrieve these event-logs from the system through a long-polling mechanism.

In order to be notified of events, the client has to perform a long-polling request towards the API Server. On reception of such long-polling request, the server does not return the HTTP response immediately \(unless error handling\): the server returns the HTTP response either when an event occurs \(including events information in the response\) or when a timeout occurs \(a timer being associated to the long-polling request\).

In order to permanently receive incoming events, the client should maintain long-polling connexion with the server. As a consequence, the API client should initiate another long-polling request when receiving an HTTP response from the API Server \(corresponding either to event\(s\) notification or timeout\).

The API supports long-polling and uses `ETag` and `If-None-Match` headers to detect for changes.

If the client provides an If-None-Match header that matches the data known by the server, then the request hangs open until the data changes, at which point the server can respond with new events instantly or until the timeout expires with no change, where the ECC responds with code 304 Not Modified.

The long-polling timeout value is specified with an attribute called `long-polling` with the value set to the desired timeout \(in seconds\)

The max number of events sent in the response can be governed with the `limit` parameter. It defaults to 30 if not specified and can be at most set to 100.

The `first-element` parameter can be used to list events starting from a specified sequence-number.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/events/{event-type}?long-polling=30
```

**Example Command To List 50 Events Starting With Element 1000:**

```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/events/{event-type}?limit=50&first-element=1000
```

#### Event-Type

The following are the events that are logged

| Event Type | Description |
| --- | --- |
| threshold | A threshold value has been passed for service |
| expiration | A service has expired and is invalid |
| device-change | The device, IMEI or SV parameter, has changed for the Subscription |
| network-change | The device has attached to a new mobile network |
| state-change | The Subscription state has changed |
| order | An order has completed |
| batch | A batch has completed |

Description of Events general Properties

| Name | Description |
| --- | --- |
| sequence-number | Sequence Number for this Event-Type |
| time | Timestamp when the event happend |
| iccid | The ICCID of the Subscription that this events relates to. Not relevant for batch events. |
| msisdn | The MSISDN of the Subscription that this events relates to. Not relevant for batch events. |
| imsi | The active IMSI of the Subscription that this events relates to. Not relevant for batch events. |
| type | The type of event. |

**Example Request:**

```
GET /ecc/v1/events/threshold HTTP/1.1
If-None-Match: "9f3b76784171ed59bc1df0bb9964f1df"
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZX=I
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Etag: "d3b11ce788cc203b8175af70cf8fbb41"
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121
{
  "events" : [
    {
    "sequence-number" : 1002, 
    "msisdn" : "4670312345",
    "iccid" : "89461177710001700003",
    "imsi": "244141000170000",
    "service" : "Data-0.5GB-Monthly", 
    "threshold" : "80-Percentage",
    "value" : "400 MB",
    "time" : "2016-03-10 08:02:54",
    "type" : "ThresholdEventInfo"

    }, 
    {
    "sequence-number" : 1003, 
    "msisdn" : "4670412345",
    "iccid" : "89463188899999999892",
    "imsi": "2441410001706789",
    "service" : "500-SMS-Monthly",
    "threshold" : "90-Percentage",
    "value" : "450",
    "time" : "2016-03-10 08:22:13",
    "type" : "ThresholdEventInfo"

    }
  ]
}
```

Description of Threshold Events additional Properties

| Name | Description |
| --- | --- |
| service | A string identifying the Service Id for which this threshold was reached |
| threshold | A string identifing the Threshold |
| value | The usage value for this service object |

**Sample Expiration Event**

```
"events": [
{
     "sequence-number" : 1142,
     "time" : "2016-03-10T08:22:481Z", 
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "service" : "500-SMS",
     "value" : "43",
     "type" : "ExpirationEventInfo"

}
```

Description of Expiration Events additional Properties

| Name | Description |
| --- | --- |
| service | A string identifying the Service Id for which this threshold was reached |
| value | The usage value for this service object |

**Sample Device-Change Event**

```
"events": [
{
     "sequence-number" : 2182,
     "time" : "2016-03-11T08:27:481Z", 
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "imei" : "490154203237518"
     "sv" : "23",
     "type" : "DeviceChangeEventInfo"

}
```

Description of Device-Change Events additional Properties

| Name | Description |
| :--- | :--- |
| imei | A string identifying the International Mobile Equipment Identity \(IMEI\). |
| sv | A string identifying the IMEI software version. |

**Sample Network-Change Event:**

```
"events": [
{
     "sequence-number" : 99,
     "time" : "2016-03-10T08:22:481Z", 
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "mcc" : "240",
     "mnc" : "006",
     "domain" : "cs",
     "type" : "NetworkChangeEventInfo"        
},
{     
     "sequence-number" : 98,
     "time" : ""2016-03-10T08:22:132Z",
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "mcc" : "240",
     "mnc" :"006",
     "domain" : "ps",
     "type" : "NetworkChangeEventInfo"
}
```

Description of Network-Change Event additional Properties

| Name | Description |
| --- | --- |
| mcc | This parameter represents the value of the MCC the subscription attach to |
| mnc | This parameter represents the value of the MNC the subscription attach to |
| domain | String identifying the type of network the subscription attached to may be "cs", "ps" or "eps" |

**Sample State-Change Event:**

```
"events": [
{
     "sequence-number" : 1002,
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "previous-state" : "BEFORE_FIRST_USE",
     "new-state" : "IN_USE",
     "time" : "2016-03-10 08:22:13",
     "type" : "StateChangeEventInfo"
}
```

Description of State-Change Event additional Properties

| Name | Description |
| --- | --- |
| previous-state | String identifying the previous state |
| new-state | String identifying the new state |

**Sample Order Event:**

```
"events": [
{
     "sequence-number" : 1002,
     "msisdn" : "4670312345",
     "iccid" : "89461177710001700003",
     "orderid" : "10032",
     "status" : "completed",
     "time" : "2016-03-10 08:22:13",
     "type" : "OrderEventInfo"     
},
{
     "sequence-number" : 1003,
     "msisdn" : "4670312346",
     "iccid" : "89461177710001700004",
     "orderid" : "10033",
     "batchid" : "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
     "status" : "completed",
     "time" : "2016-03-10 08:22:13",
     "requestid" : "931",
     "type" : "OrderEventInfo"
}
```

Note that order events related to requests submitted in a batch also contains the _batchid_ parameter and _requestid_.

Description of Orders Events additional Properties

| Name | Description |
| --- | --- |
| orderid | Order Id |
| batchid | Optional Batch Id, if the order was created as part of an API request submitted in a batch |
| status | Status of the finished order. Completed |
| requestid | Optional request id, if the order was created as part of an API request submitted in a batch and a request id was included in the batch request. |

**Sample Batch Event:**

```
"events": [
{
     "sequence-number" : 1002,
     "batchid" : "f81d4fae-7dec-11d0-a765-00a0c91e6bf6",
     "status" : "completed",
     "time" : "2016-03-10 08:22:13",
     "type" : "BatchEventInfo"     
}
```

Description of Orders Events additional Properties

| Name | Description |
| --- | --- |
| batchid | Batch Id |
| status | Status of the finished batch. Processing, Completed or Partially\_Completed |

If no events occurs for the specified long-polling timeout, the server times out the request and responds with 304:

```
HTTP/1.1 304 Not Modified
Server: Nobill/5.3.0
Etag: "d3b11ce788cc203b8175af70cf8fbb41"
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 0
```

The client can check for updates by performing the same request again, including an If-None-Match header containing  
the value of the ETag header received in the previous response from the server

```
GET /ecc/v1/subscriptions/event/threshold HTTP/1.1
If-None-Match: "d3b11ce788cc203b8175af70cf8fbb41"
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZX=I
User-Agent: curl/7.43.0
Accept: application/json
```



