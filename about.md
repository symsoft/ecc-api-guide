## API philosophy

The ECC API is a REST (ref needed) API.

Formally described in Swagger format (see chapter [API Specification](swagger_specification.md)).

Using HTTP over TLS with JSON payload.

The book describes version 0.4.0 of the API. 

The API is covered by Apache 2.0 License.

### Authentication

Basic Authentication, but also a Cookie based mechanism (describe /login and /logout URLs).

__TODO: Write a paragraph about cookies, load balancing and token expiry.__


