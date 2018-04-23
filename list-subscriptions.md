### List Subscriptions

Subscriptions can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions_ path.

The response contains a list of Subscriptions with the following fields populated per subscription:

* msisdn
* iccid
* blocked
* imsi
* subscription-type
* odb-profile
* ongoing-orders

See [Get Basic Subscription Information](/get_basic_subscription_information.md) and [List Assigned Services with Usage Details ](/list_assigned_services_with_usage_details.md)for information on how to retrieve the rest of the data for a subscription.

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

The subscriptions are by default sorted by iccid but it is possible to change this by adding an `order-by` query parameter that controls the field that should be used for sorting.

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?order-by=msisdn
```

The following fields can be used for sorting:

* iccid
* msisdn
* blocked

It is possible to sort on more than one field by including more than one `order-by` query parameter in the request. The subscription list will then be sorted on the first field and then the next field etc.

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?order-by=blocked&order-by=msisdn
```

Sort order is by default ascending, but this can be controlled by suffixing the field with `:asc` \(ascending\) or `:desc` \(descending\).

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?order-by=iccid:asc
```

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?order-by=msisdn:desc
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

#### Filtering

It is possible to filter the subscriptions by including the field as a query parameter in the request and then specifying the value that should be used for matching as the query parameter value. By default an exact match will be used when filtering subscriptions.

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?blocked=true
```

Some fields also support prefix matching and this is indicated by prefixing the parameter value with `prefix:`. The prefix must be at least 1 digit.

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?msisdn=prefix:46708
```

The following fields can be used as a filter:

| Field | Filtering type |
| :--- | :--- |
| iccid | Exact or prefix matching |
| msisdn | Exact or prefix matching |
| blocked | Exact match using 'true' or 'false' |

It is possible to filter on multiple fields by including multiple fields in the query. The query will then only return subscriptions that matches all of the given filters. It is not possible to include a field multiple times.

Example:

```
https://api.ecc.symsoft.com/ecc/v1/subscriptions?blocked=true&msisdn=prefix:46708
```

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions?iccid=prefix:8946117771&msisdn=prefix:4670842&blocked=true
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



