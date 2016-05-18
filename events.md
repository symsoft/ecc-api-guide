### Events

Events are a ECC feature that provides comprehensive event-logging for ECC Subscription.

For example, Events log when a Subscription pass a threshold, change state, change mobile network, change device, and so on.

The Events resource provides an API to retreive these event-logs.

The API supports long-polling and uses `ETag` and `If-None-Match` headers to detect for changes. 

If the client provides an If-None-Match header that matches the data known by the server, then the request hangs open until the data changes, at which point the server can respond with new data instantly. If enough time passes with no change, the ECC responds with code 304 Not Modified.
