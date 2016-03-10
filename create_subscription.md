### Create a Subscription

Text and example goes here

POST on /ecc/v1/subscriptions

Sample request:
```
todo: header

{
  "msisdn": "46708421488",
  "iccid": "89461177710001700003"
}
```

Response:
```
todo: header

{
  "msisdn": "46708421488",
  "iccid": "89461177710001700003",
  "blocked": false
}
```

__Note:__ In the current version of the API it is the responsibility of the User to allocate and keep track of MSISDNs. 