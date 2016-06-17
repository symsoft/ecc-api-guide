## API Specification

The formal ECC API specification in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format.

```yaml
---
{

    "swagger": "2.0",
    "info": {
        "description": "Symsoft Enterprise Communications Cloud API",
        "version": "pre-v0.6.0",
        "title": "ECC API",
        "termsOfService": "http://symsoft.com/api-terms/",
        "contact": {
            "email": "info@symsoft.com"
        },
        "license": {
            "name": "Apache 2.0",
            "url": "http://www.apache.org/licenses/LICENSE-2.0.html"
        }
    },
    "basePath": "/ecc/v1",
    "tags": [
        {
            "name": "Subscription",
            "description": "Operations related to Subscriptions"
        },
        {
            "name": "Service",
            "description": "Operations related to Services"
        },
        {
            "name": "SIM",
            "description": "Operations related to SIM cards"
        },
        {
            "name": "Order",
            "description": "Operations related to Orders"
        },
        {
            "name": "Event",
            "description": "Operations related to Event Streams"
        },
        {
            "name": "X-EXPERIMENTAL"
        },
        {
            "name": "Mobile Network"
        }
    ],
    "paths": {
        "/events/{event-type}": {
            "get": {
                "tags": [
                    "Event"
                ],
                "summary": "Read Events",
                "description": "TODO: more info here",
                "operationId": "read",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "event-type",
                        "in": "path",
                        "description": "The type of event",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "name": "limit",
                        "in": "query",
                        "required": false,
                        "type": "integer",
                        "format": "int32"
                    },
                    {
                        "name": "first-element",
                        "in": "query",
                        "required": false,
                        "type": "integer",
                        "format": "int64"
                    },
                    {
                        "name": "long-polling",
                        "in": "query",
                        "required": false,
                        "type": "integer",
                        "format": "int32"
                    },
                    {
                        "name": "If-None-Match",
                        "in": "header",
                        "required": false,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation"
                    },
                    "404": {
                        "description": "No queue for event type"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/hlr/{msisdn}": {
            "get": {
                "tags": [
                    "X-EXPERIMENTAL"
                ],
                "summary": "List HLR information for MSISDN",
                "description": "List basic HLR information.",
                "operationId": "read",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "msisdn",
                        "in": "path",
                        "description": "The MSISDN (E.164 number) of the Subscription",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "type": "string"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/orders/{id}": {
            "get": {
                "tags": [
                    "Order"
                ],
                "summary": "Find order",
                "description": "",
                "operationId": "get",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "id",
                        "in": "path",
                        "description": "ID of order to be fetched",
                        "required": true,
                        "type": "integer",
                        "format": "int32"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/OrderExtData"
                        }
                    },
                    "404": {
                        "description": "Order not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/services": {
            "get": {
                "tags": [
                    "Service"
                ],
                "summary": "List Subscription Types and Services available to API user",
                "description": "",
                "operationId": "read",
                "produces": [
                    "application/json"
                ],
                "parameters": [ ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionTypeServiceInfoList"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/sims": {
            "get": {
                "tags": [
                    "SIM"
                ],
                "summary": "Find SIMs",
                "description": "",
                "operationId": "find",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "limit",
                        "in": "query",
                        "required": false,
                        "type": "integer",
                        "format": "int32"
                    },
                    {
                        "name": "firstelement",
                        "in": "query",
                        "required": false,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SimExtData"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "post": {
                "tags": [
                    "SIM"
                ],
                "summary": "Create SIM",
                "description": "",
                "operationId": "create",
                "consumes": [
                    "application/json"
                ],
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "in": "body",
                        "name": "body",
                        "description": "SIM to be added",
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/SimPrototype"
                        }
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SimExtData"
                        }
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/sims/{iccid}": {
            "get": {
                "tags": [
                    "SIM"
                ],
                "summary": "Find one SIM",
                "description": "",
                "operationId": "get",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "iccid",
                        "in": "path",
                        "description": "ID of SIM to be fetched",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SimExtData"
                        }
                    },
                    "404": {
                        "description": "SIM not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "delete": {
                "tags": [
                    "SIM"
                ],
                "summary": "Delete unused SIM",
                "description": "",
                "operationId": "delete",
                "parameters": [
                    {
                        "name": "iccid",
                        "in": "path",
                        "description": "ICCID of SIM to be deleted",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "204": {
                        "description": "Successful operation"
                    },
                    "404": {
                        "description": "SIM not found"
                    },
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions": {
            "post": {
                "tags": [
                    "Subscription"
                ],
                "summary": "Create Subscription",
                "description": "Create a new Subscription and associate with a SIM (identified by ICCID) and an optional MSISDN.",
                "operationId": "create",
                "consumes": [
                    "application/json"
                ],
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "in": "body",
                        "name": "body",
                        "description": "Attributes of Subscription to be created",
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPrototype"
                        }
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}": {
            "get": {
                "tags": [
                    "Subscription"
                ],
                "summary": "List Subscription information",
                "description": "List basic Subscription information. For info about assigned Services, use the listServices operation",
                "operationId": "read",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "delete": {
                "tags": [
                    "Subscription"
                ],
                "summary": "Delete Subscription",
                "description": "Delete a Subscription and resources held, such as SIM and MSISDN. Assigned Services will also be deleted.",
                "operationId": "delete",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "patch": {
                "tags": [
                    "Subscription"
                ],
                "summary": "Update Subscription",
                "description": "Change one or several Subscription attributes, such as SIM (identified by ICCID), MSISDN or blocking state.",
                "operationId": "update",
                "consumes": [
                    "application/json"
                ],
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "in": "body",
                        "name": "body",
                        "description": "Subscription attributes to be changed",
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPatch"
                        }
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/mobile-network": {
            "get": {
                "tags": [
                    "Mobile Network"
                ],
                "summary": "List mobile network information regarding Subscription",
                "description": "",
                "operationId": "mobile_network",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/MobileNetwork"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/services": {
            "get": {
                "tags": [
                    "Service"
                ],
                "summary": "List Services assigned to Subscription",
                "description": "List Services assigned to Subscription. Services may have optional attributes.",
                "operationId": "list",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionServiceInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "post": {
                "tags": [
                    "Service"
                ],
                "summary": "Assign Services to a Subscription",
                "description": "Assign Services to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "operationId": "add",
                "consumes": [
                    "application/json"
                ],
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "in": "body",
                        "name": "body",
                        "description": "List of Services to be added",
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/ServiceListPrototype"
                        }
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/services/{sid}": {
            "post": {
                "tags": [
                    "Service"
                ],
                "summary": "Assign a Service to a Subscription",
                "description": "Assign a Service to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "operationId": "add",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "name": "sid",
                        "in": "path",
                        "description": "Service identifier",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            },
            "delete": {
                "tags": [
                    "Service"
                ],
                "summary": "Remove a Service from a Subscription",
                "description": "Remove a Service from a Subscription. All Service instances with the given identifier will be removed.",
                "operationId": "removeAll",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "name": "sid",
                        "in": "path",
                        "description": "Service identifier",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/services/{sid}/{instance}": {
            "delete": {
                "tags": [
                    "Service"
                ],
                "summary": "Remove a Service Instance from a Subscription",
                "description": "Remove a specific Service instance from a Subscription.",
                "operationId": "removeOne",
                "produces": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "name": "type",
                        "in": "path",
                        "description": "The type of identifier used",
                        "required": true,
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ]
                    },
                    {
                        "name": "id",
                        "in": "path",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "name": "sid",
                        "in": "path",
                        "description": "Service identifier",
                        "required": true,
                        "type": "string"
                    },
                    {
                        "name": "instance",
                        "in": "path",
                        "description": "Instance identifier",
                        "required": true,
                        "type": "string"
                    }
                ],
                "responses": {
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    },
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "404": {
                        "description": "Subscription not found"
                    }
                },
                "security": [
                    {
                        "basic_auth": [ ]
                    }
                ]
            }
        }
    },
    "securityDefinitions": {
        "basic_auth": {
            "type": "basic"
        }
    },
    "definitions": {
        "ServicePrototype": {
            "type": "object",
            "required": [
                "id"
            ],
            "properties": {
                "id": {
                    "type": "string",
                    "description": "Service Id"
                },
                "limit": {
                    "type": "integer",
                    "format": "int32",
                    "description": "Optional service limit"
                }
            },
            "description": "Service to be added"
        },
        "SubscriptionTypeServiceInfoList": {
            "type": "object",
            "required": [
                "api-user",
                "subscription-types"
            ],
            "properties": {
                "api-user": {
                    "type": "string",
                    "description": "API user identifier",
                    "readOnly": true
                },
                "subscription-types": {
                    "type": "array",
                    "description": "List of available subecription types with services",
                    "readOnly": true,
                    "items": {
                        "$ref": "#/definitions/SubscriptionTypeServiceInfo"
                    }
                }
            },
            "description": "Subscription Type with associated Services"
        },
        "SimExtData": {
            "type": "object",
            "required": [
                "adm",
                "iccid",
                "imsi",
                "in-use",
                "ki",
                "kic",
                "kid",
                "profile",
                "transport-key-index"
            ],
            "properties": {
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "Unique SIM identifier, usually printed on the SIM card"
                },
                "imsi": {
                    "type": "string",
                    "example": "244141000170000",
                    "description": "Primary IMSI number"
                },
                "imsi2": {
                    "type": "string",
                    "example": "240141000990000",
                    "description": "Secondary IMSI number"
                },
                "puk": {
                    "type": "string",
                    "example": "12345678",
                    "description": "Primary PUK"
                },
                "puk2": {
                    "type": "string",
                    "example": "87654321",
                    "description": "Secondary PUK"
                },
                "pin": {
                    "type": "string",
                    "example": "0000",
                    "description": "Primary PIN"
                },
                "pin2": {
                    "type": "string",
                    "example": "5678",
                    "description": "Secondary PIN"
                },
                "adm": {
                    "type": "string",
                    "example": "90223812",
                    "description": "ADM code"
                },
                "ki": {
                    "type": "string",
                    "example": "C44033360FB583130F93CD8FC7808B48",
                    "description": "Primary encryption key (encrypted by Transport Key identified by Index)"
                },
                "kic": {
                    "type": "string",
                    "example": "10A21B5B07261519A5F6996E0E045652",
                    "description": "The C encryption key (encrypted by Transport Key identified by Index)"
                },
                "kid": {
                    "type": "string",
                    "example": "E82E366A7AEFA594D98AFEA4D930308E",
                    "description": "The D encryption key (encrypted by Transport Key identified by Index)"
                },
                "profile": {
                    "type": "string",
                    "example": "ABC",
                    "description": "SIM production profile"
                },
                "transport-key-index": {
                    "type": "integer",
                    "format": "int32",
                    "example": 4,
                    "description": "Transport Key Index (identifies key used to encrypt keys)"
                },
                "in-use": {
                    "type": "boolean",
                    "description": "If SIM card is in use or reserved",
                    "default": false
                }
            }
        },
        "SubscriptionPatch": {
            "type": "object",
            "properties": {
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the new SIM to be used for the Subscription"
                },
                "msisdn": {
                    "type": "string",
                    "example": "46708421488",
                    "description": "The new MSISDN (E.164 number) of the Subscription"
                },
                "blocked": {
                    "type": "boolean",
                    "description": "If the Subscription is blocked or not",
                    "default": false
                },
                "state": {
                    "type": "string",
                    "example": "IN_USE",
                    "description": "The new state of the subscription"
                }
            },
            "description": "Subscription attributes to be changed"
        },
        "ServiceListPrototype": {
            "type": "object",
            "required": [
                "services"
            ],
            "properties": {
                "services": {
                    "type": "array",
                    "description": "List of services",
                    "items": {
                        "$ref": "#/definitions/ServicePrototype"
                    }
                }
            },
            "description": "List of Services"
        },
        "MobileNetwork": {
            "type": "object",
            "required": [
                "cs-node",
                "eps-node",
                "imsi",
                "mcc-mnc",
                "ps-node"
            ],
            "properties": {
                "imsi": {
                    "type": "string",
                    "description": "The current IMSI"
                },
                "cs-node": {
                    "type": "string",
                    "description": "CS node",
                    "readOnly": true
                },
                "ps-node": {
                    "description": "PS node",
                    "readOnly": true,
                    "$ref": "#/definitions/NodeIdentity"
                },
                "eps-node": {
                    "description": "EPS node",
                    "readOnly": true,
                    "$ref": "#/definitions/NodeIdentity"
                },
                "mcc-mnc": {
                    "type": "string",
                    "description": "MCC MNC",
                    "readOnly": true
                }
            },
            "description": "Mobile network information"
        },
        "DiagnosticInfo": {
            "type": "object",
            "required": [
                "info"
            ],
            "properties": {
                "info": {
                    "type": "string",
                    "description": "Human readable diagnostic information to aid in trouble shooting"
                }
            },
            "description": "Diagnostic Information"
        },
        "SimPrototype": {
            "type": "object",
            "required": [
                "adm",
                "iccid",
                "imsi",
                "ki",
                "kic",
                "kid",
                "profile",
                "transport-key-index"
            ],
            "properties": {
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "Unique SIM identifier, usually printed on the SIM card"
                },
                "imsi": {
                    "type": "string",
                    "example": "244141000170000",
                    "description": "Primary IMSI number"
                },
                "imsi2": {
                    "type": "string",
                    "example": "240141000990000",
                    "description": "Secondary IMSI number"
                },
                "puk": {
                    "type": "string",
                    "example": "12345678",
                    "description": "Primary PUK"
                },
                "puk2": {
                    "type": "string",
                    "example": "87654321",
                    "description": "Secondary PUK"
                },
                "pin": {
                    "type": "string",
                    "example": "0000",
                    "description": "Primary PIN"
                },
                "pin2": {
                    "type": "string",
                    "example": "5678",
                    "description": "Secondary PIN"
                },
                "adm": {
                    "type": "string",
                    "example": "90223812",
                    "description": "ADM code"
                },
                "ki": {
                    "type": "string",
                    "example": "C44033360FB583130F93CD8FC7808B48",
                    "description": "Primary encryption key (encrypted by Transport Key identified by Index)"
                },
                "kic": {
                    "type": "string",
                    "example": "10A21B5B07261519A5F6996E0E045652",
                    "description": "The C encryption key (encrypted by Transport Key identified by Index)"
                },
                "kid": {
                    "type": "string",
                    "example": "E82E366A7AEFA594D98AFEA4D930308E",
                    "description": "The D encryption key (encrypted by Transport Key identified by Index)"
                },
                "profile": {
                    "type": "string",
                    "example": "ABC",
                    "description": "SIM production profile"
                },
                "transport-key-index": {
                    "type": "integer",
                    "format": "int32",
                    "example": 4,
                    "description": "Transport Key Index (identifies key used to encrypt keys)"
                }
            },
            "description": "Parameters required at creation of a new SIM card"
        },
        "ServiceInstanceInfo": {
            "type": "object",
            "required": [
                "id"
            ],
            "properties": {
                "id": {
                    "type": "string",
                    "description": "The Service identifier"
                },
                "instance": {
                    "type": "string",
                    "description": "Optional instance identifier"
                },
                "value": {
                    "type": "integer",
                    "format": "int64",
                    "description": "Optional value for consuming Service"
                },
                "expires": {
                    "type": "string",
                    "description": "Optional expiry date of the Service"
                }
            },
            "description": "Information about a Subscriber Service instance"
        },
        "OrderInfo": {
            "type": "object",
            "required": [
                "orders"
            ],
            "properties": {
                "orders": {
                    "type": "array",
                    "description": "List of order identifiers",
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    }
                }
            },
            "description": "List of order identifiers"
        },
        "SubscriptionInfo": {
            "type": "object",
            "required": [
                "blocked",
                "iccid",
                "imsi",
                "status",
                "subscription-type"
            ],
            "properties": {
                "msisdn": {
                    "type": "string",
                    "example": "46708421488",
                    "description": "The MSISDN (E.164 number) of the Subscription"
                },
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the SIM used by the Subscription"
                },
                "status": {
                    "type": "string",
                    "description": "Subscriber status"
                },
                "blocked": {
                    "type": "boolean",
                    "description": "If the Subscriber is blocked or not",
                    "default": false
                },
                "imsi": {
                    "type": "array",
                    "example": "244141000170000",
                    "description": "A list of IMSI numbers used by the Subscription",
                    "items": {
                        "type": "string"
                    }
                },
                "subscription-type": {
                    "type": "string",
                    "example": "The Holy Subscription",
                    "description": "Subscription type",
                    "readOnly": true
                },
                "ongoing-orders": {
                    "type": "array",
                    "example": "10049",
                    "description": "A list of Order IDs for provisioning orders in progress on the Subscription",
                    "readOnly": true,
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    }
                }
            },
            "description": "Basic information about a Subscription"
        },
        "OrderExtData": {
            "type": "object",
            "properties": {
                "msisdn": {
                    "type": "string"
                },
                "iccid": {
                    "type": "string"
                },
                "status": {
                    "type": "string"
                },
                "order-id": {
                    "type": "integer",
                    "format": "int32",
                    "readOnly": true
                },
                "order-date": {
                    "type": "string",
                    "readOnly": true
                },
                "completion-date": {
                    "type": "string",
                    "readOnly": true
                }
            }
        },
        "SubscriptionTypeServiceInfo": {
            "type": "object",
            "required": [
                "name",
                "services"
            ],
            "properties": {
                "name": {
                    "type": "string",
                    "description": "Subscription Type name"
                },
                "services": {
                    "type": "array",
                    "description": "List of available services",
                    "items": {
                        "$ref": "#/definitions/ServiceInfo"
                    }
                }
            },
            "description": "Subscription Type with associated Services"
        },
        "SubscriptionServiceInfo": {
            "type": "object",
            "required": [
                "services"
            ],
            "properties": {
                "msisdn": {
                    "type": "string",
                    "example": "46708621488",
                    "description": "The new MSISDN (E.164 number) of the Subscription"
                },
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "Unique SIM identifier, usually printed on the SIM card"
                },
                "services": {
                    "type": "array",
                    "description": "List of assigned services",
                    "items": {
                        "$ref": "#/definitions/ServiceInstanceInfo"
                    }
                }
            },
            "description": "Detailed Service information for a Subscription"
        },
        "ServiceInfo": {
            "type": "object",
            "required": [
                "id"
            ],
            "properties": {
                "id": {
                    "type": "string",
                    "description": "The Service identifier"
                },
                "description": {
                    "type": "string",
                    "description": "Optional description"
                }
            },
            "description": "Information about a Service"
        },
        "SubscriptionPrototype": {
            "type": "object",
            "required": [
                "iccid",
                "subscription-type"
            ],
            "properties": {
                "iccid": {
                    "type": "string",
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the SIM to be used for the Subscription"
                },
                "msisdn": {
                    "type": "string",
                    "example": "46708421488",
                    "description": "The MSISDN (E.164 number) of the Subscription"
                },
                "subscription-type": {
                    "type": "string",
                    "example": "The Holy Subscription",
                    "description": "Subscription type"
                }
            },
            "description": "Parameters required at creation of a new Subscription"
        },
        "NodeIdentity": {
            "type": "object",
            "properties": {
                "number": {
                    "type": "string",
                    "description": "Optional instance identifier"
                },
                "host": {
                    "type": "string",
                    "description": "Optional instance identifier"
                },
                "realm": {
                    "type": "string",
                    "description": "Optional instance identifier"
                }
            },
            "description": "Node identity"
        }
    }

}
```

