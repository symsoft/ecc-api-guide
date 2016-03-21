### Example Services

A simple set of Services (defined at [onboarding](onboarding.md)) could look like: 

 * __FreeZoneData__ - Free data access to walled garden.
 
 * __DataMonthly1G__ - Recurring data service bucket of 1G. Reset at the 1st day of each month. Only one recurring data service allowed.

 * __DataMonthly5G__ - Recurring data service bucket of 5G. Reset at the 1st day of each month. Only one recurring data service allowed.

 * __Data1G__ - Data service bucket of 1G. Expires after 6 months. Multiple instances allowed. Recurring bucket has precedence. Oldest bucket used first.

 * __Data5G__ - Data service bucket of 5G. Expires after 6 months. Multiple instances allowed. Recurring bucket has precedence. Oldest bucket used first.

 * __Voice__ - Voice call service. Each call charged individually.

 * __SMS__ - Short message service. Each SMS charged individually.


__Example Subscription using Services above:__

```
{
  "msisdn" : "46708421488",
  "services" : [ {
    "id" : "Voice"
  }, {
    "id" : "SMS"
  }, {
    "id" : "FreeZoneData"
  }, {
    "id" : "Data1G",
    "instance" : "b78",
    "value" : 1000,
    "expires" : "Thu Mar 22 18:50:23 CET 2016"
  }, {
    "id" : "Data1G",
    "instance" : "a77",
    "value" : 556,
    "expires" : "Thu Mar 16 10:20:11 CET 2016"
  }, {
    "id" : "DataMonthly1G",
    "value" : 0
  } ]
}
```

