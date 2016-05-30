### Events

Events are a ECC feature that provides comprehensive event-logging for ECC Subscription.

A number of events are supported, for example, when a usage threshold is passed, state change, mobile network change, device change, and so on.

The Events resource provides an API to retreive these event-logs from the system through a long-polling mechanism.

In order to be notified of events, the client has to perform a long-polling request towards the API Server. On reception of such long-polling request, the server does not return the HTTP response immediately (unless error handling): the server returns the HTTP response either when an event occurs (including events information in the response) or when a timeout occurs (a timer being associated to the long-polling request). 

In order to permanently receive incoming events, the client should maintain long-polling connexion with the server. As a consequence, the API client should initiate another long-polling request when receiving an HTTP response from the API Server (corresponding either to event(s) notification or timeout).

The API supports long-polling and uses `ETag` and `If-None-Match` headers to detect for changes.  

If the client provides an If-None-Match header that matches the data known by the server, then the request hangs open until the data changes, at which point the server can respond with new events instantly or until the timeout expires with no change, where the ECC responds with code 304 Not Modified.

The long-polling timeout value is specified with a attribute called `long-polling` with the value set to the desired timeout (in seconds)

__Example Command:__
```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/events/{event-type}?long-polling=30
```
####Event-Type

The following are the events that are logged

| Event Type | Description |
|------------|--------|
| threshold | A threshold value has been passed for service |
| device-change | The device, IMEI or SV parameter, has changed for the Subscription |
| network-change | The device has attached to a new mobile network |
| state-change | The Subscrition state has changed| 




__Example Request:__
```
GET /ecc/v1/subscriptions/event/threshold HTTP/1.1
If-None-Match: "9f3b76784171ed59bc1df0bb9964f1df"
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZX=I
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
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
    "sequence-number" : 1002 
    "msisdn" : "4670312345"
    "iccid" : "89461177710001700003"
    "imsi": "244141000170000"
    "service" : "data" 
    "threshold" : "
    "value" :
    "time" :
    }, 
    {
    "sequence-number" : 1003 
    "msisdn" : ""
    "iccid" : "89463188899999999892"
    "imsi": "2441410001706789"
    "service" : 
    "threshold" : 
    "value" :
    "time" :
    }
  ]
}
```

If no events occurs for the specified long-polling timeout, the server times out the request and responds with 304:

```
HTTP/1.1 304 Not Modified
Server: Nobill/5.3.0
Etag: "d3b11ce788cc203b8175af70cf8fbb41"
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 0
```
The client can check for updates by performing the same request again, including an If-None-Match header containing the value of the ETag header received in the previous response from the server

```
GET /ecc/v1/subscriptions/event/threshold HTTP/1.1
If-None-Match: "d3b11ce788cc203b8175af70cf8fbb41"
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZX=I
User-Agent: curl/7.43.0
Accept: application/json
```
