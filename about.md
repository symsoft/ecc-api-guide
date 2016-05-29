## API philosophy

The Enterprise Communications Cloud (ECC) API is a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) API.

The API uses HTTP over TLS with [JSON payload](payload.md).

Operations that change subscription state such as POST/PATCH/DELETE are asynchronous (returns 202, Accepted) and will eventually be executed. 

The normative API reference is the specification in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format (see chapter [API Specification](swagger_specification.md)). This book describes version 0.6.0 of the API.

The API is covered by [Apache 2.0 License](license.md).


