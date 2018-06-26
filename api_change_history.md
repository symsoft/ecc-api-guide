## API change history

## 1.4.0

* Add support for retrieving the [cell-id](/get_mobile_network.md)
*  Insignificant changes in the returned JSON objects:
  * Optional fields with null values are not included \(this was a bit inconsistent in the previous releases\)
  * Extra white space is not included in the JSON \(it was previously "pretty-printed"\)

## 1.3.0

* Add support for [listing subscriptions](/list-subscriptions.md)
* Add support for [tags](/tags.md)
* Add main-imsi to [Get Basic Subscription Information](/get_basic_subscription_information.md)

## 1.2.0

* Define the order statuses
* Allow sid to be specified in the resource parameter in a batch request

## 1.1.1

* Removed 'readOnly' properties from swagger definition

## 1.1.0

* Added support for specifying APN identifiers per subscription

## 1.0.1

* Added IMEI and SV to device-change event.

## 1.0.0

* Public release



