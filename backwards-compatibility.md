### Backwards compatibility

An ECC client must follow some guidelines to be backwards compatible.

How to do this:

* Ignore new and unknown fields in the payload \(regardless of the absence of an additionalProperties declaration\).
* Be prepared for new enum values declared with x-extensible-enum; provide default behaviour for unknown values, if applicable.
* Follow the redirect when the server returns an “HTTP 301 Moved Permanently” response code.
* Be prepared to handle HTTP status codes not explicitly specified in endpoint definitions! Note also, that status codes are extensible – default handling is how you would treat the corresponding x00 code \(see RFC7231 Section 6\).
* Fields not declared as mandatory in the payload may be excluded
* Do not rely on a specific formatting on the payload
  * Fields may be in a different order in the payload
  * White space may be included in the payload





