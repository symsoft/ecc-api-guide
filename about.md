## API philosophy

The Enterprise Communications Cloud (ECC) API is a _pragmatic_ [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) API.

Using HTTP over TLS with JSON payload.

POST/PATCH/DELETE operations are asynchronous (returns 202) and will eventually be executed.

The book describes version 0.4.0 of the API. 

Formally described in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format (see chapter [API Specification](swagger_specification.md)).

The API is covered by [Apache 2.0 License](license.md).


