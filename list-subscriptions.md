### List Subscriptions

Subscriptions can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions_ path.

The response contains of a list of Subscriptions with limited information. See [Get Basic Subscription Information](/get_basic_subscription_information.md) and [List Assigned Services with Usage Details ](/list_assigned_services_with_usage_details.md)for information on how to retrieve the rest of the data for a subscription.

The subscriptions are by default sorted by ICCID and the returned list of subscriptions is limited to at most 100 subscriptions. The request supports paging to make it possible to retrieve more than 100 subscriptions.

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions
```

**Example Response:**

```
{
  "subscriptions" : [ {
    "msisdn" : "46708421488",
    "iccid" : "89461177710001700003",
    "blocked" : false,
    "imsi" : [ "244141000170000" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  }, {
    "msisdn" : "46708421489",
    "iccid" : "89461177710001700004",
    "blocked" : false,
    "imsi" : [ "244141000170001" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  } ]
}
```

#### Sorting

It is possible to change how the subscriptions should be sorted by adding an `order-by` query parameter that specifies the field that should be used for sorting. If more than one `order-by` query parameter is specified the result will first be sorted on the first field and then the next field etc.

The following fields can be used for sorting:

* iccid
* msisdn
* blocked

Sort order is by default ascending, but this can be controlled by suffixing the field with `:asc` \(ascending\) or `:desc` \(descending\).

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?order-by=iccid:asc&order-by=msisdn:desc
```

**Example Response:**

```
{
  "subscriptions" : [ {
    "msisdn" : "46708421488",
    "iccid" : "89461177710001700003",
    "blocked" : false,
    "imsi" : [ "244141000170000" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  }, {
    "msisdn" : "46708421489",
    "iccid" : "89461177710001700004",
    "blocked" : false,
    "imsi" : [ "244141000170001" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  } ]
}Filtering
```

#### Filtering

It is possible to filter the returned subscriptions by including the following query parameters in the request:

| Query parameter | Description |
| :--- | :--- |
| iccid-prefix | Match subscriptions with an iccid starting with these digits |
| msisdn-prefix | Match subscriptions with an msisdn starting with these digits |
| blocked | Is the subscription blocked true/false |

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?iccid-prefix=8946117771&msisdn-prefix=4670842&blocked=true
```

**Example Response:**

```
{
  "subscriptions" : [ {
    "msisdn" : "46708421488",
    "iccid" : "89461177710001700003",
    "blocked" : false,
    "imsi" : [ "244141000170000" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  }, {
    "msisdn" : "46708421489",
    "iccid" : "89461177710001700004",
    "blocked" : false,
    "imsi" : [ "244141000170001" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  } ]
}
```

#### Paging

It is possible to control paging by using the `offset` and `limit` query parameters. These parameters specifies what part/page of the subscriptions that should be returned.

| Query parameter | Description |
| :--- | :--- |
| limit | Max number of subscriptions returned. Max value is 100 and the default is 100. |
| offset | Offset for the first returned subscription. |

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?offset=0&limit=2
```

**Example Response:**

```
{
  "subscriptions" : [ {
    "msisdn" : "46708421488",
    "iccid" : "89461177710001700003",
    "blocked" : false,
    "imsi" : [ "244141000170000" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  }, {
    "msisdn" : "46708421489",
    "iccid" : "89461177710001700004",
    "blocked" : false,
    "imsi" : [ "244141000170001" ],
    "subscription-type" : "Blue",
    "odb-profile" : 10,
    "ongoing-orders" : [ ]
  } ]
}
```



