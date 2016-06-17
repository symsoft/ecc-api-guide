## Services

Services are a collection of applications and features available to mobile subscribers or devices. 
Services specifies which capabilities, such as voice and sms, a subscription may utilize and also controls the usage of the corresponding network resources.
The available services for an API User is specified during the on-boarding process.

The following service types are available: 

| Service Type | Description |
|------------|--------|
| teleservice |  specifies which capabilities, Voice, Mobile Originated SMS and Mobile Terminated SMS a subscription may use |
| supplementary-service | Supplementary services, such as call forwarding, call barring for voice services |
| bucket | services which monitors usage consumption for different resorces |
| reccuring-bucket | bucket services that are automatically renewed |

Services are identified by the _[sid](parameters.md#msid)_ . For teleservices and supplemenatry-services the sid is defined and the same for all API Users.

####Teleservices

The following capabillities are available and identified by _[sid](parameters.md#msid)_, "ts-voice", "ts-mo-sms" and "ts-mt-sms".

####Supplementary services
The following supplementary services are available and identified by _[sid](parameters.md#msid)_ "cfu", "cfb", "cfnr", "cfnrc", "clip", "clir" and "mpty".

For the call-forwarding supplementarty services "cfu", "cfb", "cfnr" and "cfnrc" an additional parameter "forward-number" is available.

The following service section allows a subscription to use voice and sms and has the supplementary service call forwarding not reached and calling line restriction activated: 
```
{
  ...
  "services" : [ {
    "id" : "ts-voice"
  }, {
    "id" : "ts-sms-mo"
  }, {
    "id" : "ts-sms-mt"
  }, {
    "id" : "cfnr",
    "forward-number" : "4670123123123"
  }, {
    "id" : "clir"}]
}
```
#### Bucket and Recurring Bucket

These services are (defined at [onboarding](onboarding.md)) so the _[sid](parameters.md#msid)_ is unique per API user. 
A set of services could look like this
 
 * __DataMonthly1G__ - Recurring data service bucket of 1G. Reset at the 1st day of each month. Only one recurring data service allowed.

 * __VoiceMonthly__ - Recurring voice service bucket. Reset at the 1st day of each month. Only one recurring voice service allowed.

 * __Data1G__ - Data service bucket of 1G. Expires after 6 months. Multiple instances allowed. Recurring bucket has precedence. Oldest bucket used first.


__Example Subscription using Services above:__

```
{
  ...
  "services" : [ {
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

For recurring bucket services an optional limit can be specified. The limit are applied individual per subscription.
The service below is a recurring voice service. Reset at the 1st day of each month with an individual limit of 1000 minutes per month. Current usage is 8 minutes.

```
{
  ...
  "services" : [ {
    "id" : "VoiceMonthly",
    "limit" : "1000",
    "value" : 8,
  } ]
}
```
