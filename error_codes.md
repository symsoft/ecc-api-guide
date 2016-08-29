### Error codes

The API will return standard HTTP return codes in case of an error. In most cases there will be additional, human readable, information in the response body.

Common error cases: 

* Code 404 (Not Found) refers to the main resource, i.e. the Subscription. This is also what will be returned in case an API User tries to access a Subscription belonging to another API User.

* Code 409 (Conflict) is returned when the requested resource, such as a SIM or an MSISDN, already is in use. 

* Code 400 (Bad Request) is returned when the request refers to a non existing entity other than the main resource, or when required parameters are missing or malformed. 
