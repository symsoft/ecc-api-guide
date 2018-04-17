### List Subscriptions

Subscriptions can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions_ path.

The response contains of a list of Subscriptions with limited information. See [Get Basic Subscription Information](/get_basic_subscription_information.md) and [List Assigned Services with Usage Details ](/list_assigned_services_with_usage_details.md)for information on how to retrieve the rest of the data for a subscription.

The subscriptions are sorted by ICCID and the returned list is limited to at most 100 subscriptions. The request supports paging to make it possible to retrieve more than 100 subscriptions.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions
```

**Example Request:**

```
GET /ecc/v1/subscriptions HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 334

{
  "subscriptions": [
    {
      "msisdn" : "46708421488",
      "iccid" : "89461177710001700003",
      "blocked" : false,
      "imsi": [ "244141000170000" ]
    }
  ]
}
```

#### Paging

It is possible to add a offset and limit query parameter that specifies what part of the subscriptions that should be returned.

| Query parameter | Description |
| :--- | :--- |
| limit | Max number of subscriptions returned. Max value is 100 and the default is 100. |
| offset | Offset for the first returned subscription. |

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?offset=2&limit=2
```

**Example Request:**

```
GET /ecc/v1/subscriptions?offset=2&limit=2 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 26 Mar 2016 16:14:36 GMT
Content-Length: 334

{
  "subscriptions": [
    {
      "msisdn" : "46708421488",
      "iccid" : "89461177710001700003",
      "blocked" : false,
      "imsi": [ "244141000170000" ]
    }
  ]
}
```



