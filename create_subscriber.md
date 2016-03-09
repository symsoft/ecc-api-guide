### Create a Subscriber

Text and example goes here

POST on /ecc/v1/subscribers

Sample request:
```
todo: header

{
  "msisdn": "46708621488",
  "iccid": "89461177710001700003"
}
```

Response:
```
todo: header

{
  "msisdn": "46708621488",
  "iccid": "89461177710001700003",
  "blocked": false
}
```

__Note:__ In the current version of the API it is the responsibility of the User to allocate and keep track of MSISDNs. 