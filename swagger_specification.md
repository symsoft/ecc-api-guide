## API Specification

The formal ECC API specification in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format.

```yaml
---
{
    "swagger": "2.0",
    "info": {
        "description": "Symsoft Enterprise Communications Cloud API",
        "version": "v0.8.1",
        "title": "ECC API",
        "license": {
            "name": "Apache 2.0",
            "url": "http://www.apache.org/licenses/LICENSE-2.0.html"
        },
        "contact": {
            "email": "ecc-team@symsoft.com"
        },
        "termsOfService": "http://symsoft.com/api-terms/"
    },
    "basePath": "/ecc/v1",
    "tags": [
        {
            "description": "Operations related to Subscriptions",
            "name": "Subscription"
        },
        {
            "description": "Operations related to Services",
            "name": "Service"
        },
        {
            "description": "Operations related to Orders",
            "name": "Order"
        },
        {
            "description": "Operations related to Event Streams",
            "name": "Event"
        },
        {
            "name": "Batch"
        },
        {
            "name": "Mobile Network"
        }
    ],
    "paths": {
        "/subscriptions/{type}:{id}/services/{sid}": {
            "patch": {
                "summary": "Modify a Service belonging to a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Modify a Service that's assigned to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Service"
                ],
                "operationId": "modifyService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service identifier",
                        "name": "sid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "New data for service",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/ServicePrototypeExternalSid"
                        },
                        "in": "body",
                        "required": false
                    }
                ]
            },
            "delete": {
                "summary": "Remove a Service from a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Remove a Service from a Subscription. All Service instances with the given identifier will be removed.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Service"
                ],
                "operationId": "removeAllServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service identifier",
                        "name": "sid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            },
            "get": {
                "summary": "List service details for a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "List details of a service assigned to a subscription. Services may have optional attributes.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionServiceInfo"
                        }
                    }
                },
                "tags": [
                    "Service"
                ],
                "operationId": "getServiceDetails",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service identifier",
                        "name": "sid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            },
            "post": {
                "summary": "Assign a Service to a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Assign a Service to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Service"
                ],
                "operationId": "addService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service identifier",
                        "name": "sid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service settings",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/ServicePrototypeExternalSid"
                        },
                        "in": "body",
                        "required": false
                    }
                ]
            }
        },
        "/events/{event-type}": {
            "get": {
                "summary": "Read Events",
                "produces": [
                    "application/json"
                ],
                "description": "List events of a specific type.",
                "responses": {
                    "404": {
                        "description": "No queue for event type"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/EventListInfo"
                        }
                    }
                },
                "tags": [
                    "Event"
                ],
                "operationId": "getEventTypeChange",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of event",
                        "name": "event-type",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "format": "int32",
                        "name": "limit",
                        "type": "integer",
                        "in": "query",
                        "required": false
                    },
                    {
                        "format": "int64",
                        "name": "first-element",
                        "type": "integer",
                        "in": "query",
                        "required": false
                    },
                    {
                        "format": "int32",
                        "name": "long-polling",
                        "type": "integer",
                        "in": "query",
                        "required": false
                    },
                    {
                        "name": "If-None-Match",
                        "type": "string",
                        "in": "header",
                        "required": false
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/mobile-network": {
            "get": {
                "summary": "List mobile network information regarding Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/MobileNetwork"
                        }
                    }
                },
                "tags": [
                    "Mobile Network"
                ],
                "operationId": "getMobileNetwork",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            }
        },
        "/orders/{id}": {
            "get": {
                "summary": "Find order",
                "produces": [
                    "application/json"
                ],
                "description": "",
                "responses": {
                    "404": {
                        "description": "Order not found"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/OrderExtData"
                        }
                    }
                },
                "tags": [
                    "Order"
                ],
                "operationId": "getOrder",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "ID of order to be fetched",
                        "type": "integer",
                        "format": "int32",
                        "name": "id",
                        "in": "path",
                        "required": true
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/services/{sid}/{instance}": {
            "delete": {
                "summary": "Remove a Service Instance from a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Remove a specific Service instance from a Subscription.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Service"
                ],
                "operationId": "removeOneService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Service identifier",
                        "name": "sid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Instance identifier",
                        "name": "instance",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            }
        },
        "/subscriptions": {
            "post": {
                "summary": "Create Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Create a new Subscription and associate with a SIM (identified by ICCID) and an optional MSISDN.",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "responses": {
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Subscription"
                ],
                "operationId": "createSubscription",
                "consumes": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "description": "Attributes of Subscription to be created",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPrototype"
                        },
                        "in": "body",
                        "required": true
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}/services": {
            "get": {
                "summary": "List Services assigned to Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "List Services assigned to Subscription. Services may have optional attributes.",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionServiceInfo"
                        }
                    }
                },
                "tags": [
                    "Service"
                ],
                "operationId": "listServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            },
            "post": {
                "summary": "Assign Services to a Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Assign Services to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Service"
                ],
                "operationId": "addServices",
                "consumes": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "List of Services to be added",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/ServiceListPrototype"
                        },
                        "in": "body",
                        "required": true
                    }
                ]
            }
        },
        "/services": {
            "get": {
                "summary": "List Subscription Types and Services available to API user",
                "produces": [
                    "application/json"
                ],
                "description": "",
                "responses": {
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionTypeServiceInfoList"
                        }
                    }
                },
                "tags": [
                    "Service"
                ],
                "operationId": "getServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": []
            }
        },
        "/batches": {
            "post": {
                "summary": "Submit Batch",
                "produces": [
                    "application/json"
                ],
                "description": "Submit batch job.",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "responses": {
                    "404": {
                        "description": "No queue for event type"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/EventListInfo"
                        }
                    }
                },
                "tags": [
                    "Batch"
                ],
                "operationId": "createBatch",
                "consumes": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "description": "Attributes of Subscription to be created",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/BatchPrototype"
                        },
                        "in": "body",
                        "required": true
                    }
                ]
            }
        },
        "/subscriptions/{type}:{id}": {
            "patch": {
                "summary": "Update Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Change one or several Subscription attributes, such as SIM (identified by ICCID), MSISDN or blocking state.",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "409": {
                        "description": "Conflict",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
                    "400": {
                        "description": "Bad request",
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        }
                    },
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
                "tags": [
                    "Subscription"
                ],
                "operationId": "updateSubscription",
                "consumes": [
                    "application/json"
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "Subscription attributes to be changed",
                        "name": "body",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPatch"
                        },
                        "in": "body",
                        "required": true
                    }
                ]
            },
            "delete": {
                "summary": "Delete Subscription",
                "produces": [
                    "application/json"
                ],
                "description": "Delete a Subscription and resources held, such as SIM and MSISDN. Assigned Services will also be deleted.",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "202": {
                        "description": "Request accepted",
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        }
                    }
                },
                "tags": [
                    "Subscription"
                ],
                "operationId": "deleteSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            },
            "get": {
                "summary": "List Subscription information",
                "produces": [
                    "application/json"
                ],
                "description": "List basic Subscription information. For info about assigned Services, use the listServices operation",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/SubscriptionInfo"
                        }
                    }
                },
                "tags": [
                    "Subscription"
                ],
                "operationId": "getSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The type of identifier used",
                        "type": "string",
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "name": "type",
                        "in": "path",
                        "required": true
                    },
                    {
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "name": "id",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            }
        },
        "/batches/{uuid}": {
            "get": {
                "summary": "Read Batch",
                "produces": [
                    "application/json"
                ],
                "description": "Get batch information.",
                "responses": {
                    "404": {
                        "description": "No queue for event type"
                    },
                    "200": {
                        "description": "Successful operation",
                        "schema": {
                            "$ref": "#/definitions/BatchStatusInfo"
                        }
                    }
                },
                "tags": [
                    "Batch"
                ],
                "operationId": "getBatch",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "parameters": [
                    {
                        "description": "The batch uuid",
                        "name": "uuid",
                        "type": "string",
                        "in": "path",
                        "required": true
                    }
                ]
            }
        }
    },
    "definitions": {
        "SubscriptionTypeServiceInfoList": {
            "description": "Subscription Type with associated Services",
            "type": "object",
            "properties": {
                "api-user": {
                    "description": "API user identifier",
                    "readOnly": true,
                    "type": "string"
                },
                "subscription-types": {
                    "items": {
                        "$ref": "#/definitions/SubscriptionTypeServiceInfo"
                    },
                    "description": "List of available subscription types with services",
                    "readOnly": true,
                    "type": "array"
                }
            }
        },
        "ServiceInfo": {
            "description": "Information about a Subscriber Service instance",
            "properties": {
                "value": {
                    "description": "Optional value for consuming Service",
                    "type": "integer",
                    "format": "int64"
                },
                "limit": {
                    "description": "Optional max value for the consuming Service",
                    "type": "integer",
                    "format": "int64"
                },
                "instance": {
                    "items": {
                        "$ref": "#/definitions/ServiceInstanceInfo"
                    },
                    "description": "Optional instances",
                    "type": "array"
                },
                "id": {
                    "description": "The Service identifier",
                    "type": "string"
                },
                "reset-date": {
                    "description": "Optional reset date of the Service",
                    "readOnly": true,
                    "type": "string"
                },
                "expires": {
                    "description": "Optional expiry date of the Service",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "id"
            ]
        },
        "ServicePrototypeExternalSid": {
            "description": "Service to be added",
            "type": "object",
            "properties": {
                "limit": {
                    "description": "Optional service limit",
                    "type": "integer",
                    "format": "int32"
                },
                "forwarding-number": {
                    "description": "Optional service forwarding number",
                    "type": "string"
                }
            }
        },
        "SubscriptionServiceInfo": {
            "description": "Detailed Service information for a Subscription",
            "properties": {
                "services": {
                    "items": {
                        "$ref": "#/definitions/ServiceInfo"
                    },
                    "description": "List of assigned services",
                    "type": "array"
                },
                "msisdn": {
                    "example": "46708621488",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "type": "string"
                },
                "iccid": {
                    "example": "89461177710001700003",
                    "description": "Unique SIM identifier, usually printed on the SIM card",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "services"
            ]
        },
        "ServiceInstanceInfo": {
            "description": "Information about a Subscriber Service instance",
            "properties": {
                "value": {
                    "description": "Optional value for consuming Service",
                    "type": "integer",
                    "format": "int64"
                },
                "limit": {
                    "description": "Optional max value for the consuming Service",
                    "type": "integer",
                    "format": "int64"
                },
                "instance": {
                    "description": "Instance identifier",
                    "type": "string"
                },
                "expires": {
                    "description": "Optional expiry date of the Service",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "instance"
            ]
        },
        "BatchRequestPrototype": {
            "description": "Parameters required at creation of a new Batch request",
            "type": "object",
            "properties": {
                "method": {
                    "example": "POST",
                    "description": "The method of the request",
                    "type": "string"
                },
                "body": {
                    "description": "The body of the request",
                    "$ref": "#/definitions/BatchRequestBodyPrototype"
                },
                "requestid": {
                    "example": "1276322",
                    "description": "The id of the request",
                    "type": "string"
                },
                "resource": {
                    "example": "subscriptions",
                    "description": "The resource of the request",
                    "type": "string"
                }
            }
        },
        "SubscriptionPrototype": {
            "description": "Parameters required at creation of a new Subscription",
            "properties": {
                "msisdn": {
                    "example": "46708421488",
                    "description": "The MSISDN (E.164 number) of the Subscription",
                    "type": "string"
                },
                "subscription-type": {
                    "example": "The Holy Subscription",
                    "description": "Subscription type",
                    "type": "string"
                },
                "odb-profile": {
                    "description": "The new ODB profile",
                    "type": "integer",
                    "format": "int32"
                },
                "iccid": {
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the SIM to be used for the Subscription",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "iccid",
                "subscription-type"
            ]
        },
        "BatchOrderInfo": {
            "description": "Information about an order in a batch job",
            "type": "object",
            "properties": {
                "orderid": {
                    "description": "The order ID of the request",
                    "readOnly": true,
                    "type": "integer",
                    "format": "int32"
                },
                "info": {
                    "description": "Optional extra information about the request",
                    "readOnly": true,
                    "type": "string"
                },
                "requestid": {
                    "description": "The ID of the request",
                    "readOnly": true,
                    "type": "string"
                },
                "status": {
                    "description": "The status of the request",
                    "readOnly": true,
                    "type": "string"
                }
            }
        },
        "EventListInfo": {
            "description": "Events for a specific event type",
            "properties": {
                "events": {
                    "items": {
                        "$ref": "#/definitions/EventInfo"
                    },
                    "description": "List of events",
                    "type": "array"
                }
            },
            "type": "object",
            "required": [
                "events"
            ]
        },
        "OrderExtData": {
            "type": "object",
            "properties": {
                "status": {
                    "type": "string"
                },
                "msisdn": {
                    "type": "string"
                },
                "completion-date": {
                    "readOnly": true,
                    "type": "string"
                },
                "order-id": {
                    "readOnly": true,
                    "type": "integer",
                    "format": "int32"
                },
                "iccid": {
                    "type": "string"
                },
                "order-date": {
                    "readOnly": true,
                    "type": "string"
                }
            }
        },
        "DeviceChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about a Device Change event",
                    "type": "object",
                    "properties": {}
                }
            ]
        },
        "NodeIdentity": {
            "description": "Node identity",
            "type": "object",
            "properties": {
                "host": {
                    "description": "Optional instance identifier",
                    "type": "string"
                },
                "realm": {
                    "description": "Optional instance identifier",
                    "type": "string"
                },
                "number": {
                    "description": "Optional instance identifier",
                    "type": "string"
                }
            }
        },
        "ServiceListPrototype": {
            "description": "List of Services",
            "properties": {
                "services": {
                    "items": {
                        "$ref": "#/definitions/ServicePrototype"
                    },
                    "description": "List of services",
                    "type": "array"
                }
            },
            "type": "object",
            "required": [
                "services"
            ]
        },
        "MobileNetwork": {
            "description": "Mobile network information",
            "type": "object",
            "properties": {
                "mnc": {
                    "description": "MNC",
                    "readOnly": true,
                    "type": "string"
                },
                "ps-node": {
                    "description": "PS node",
                    "readOnly": true,
                    "$ref": "#/definitions/NodeIdentity"
                },
                "cs-node": {
                    "description": "CS node",
                    "readOnly": true,
                    "type": "string"
                },
                "imsi": {
                    "description": "The current IMSI",
                    "type": "string"
                },
                "mcc": {
                    "description": "MCC",
                    "readOnly": true,
                    "type": "string"
                },
                "eps-node": {
                    "description": "EPS node",
                    "readOnly": true,
                    "$ref": "#/definitions/NodeIdentity"
                }
            }
        },
        "EventInfo": {
            "description": "Information about an Event",
            "type": "object",
            "properties": {
                "msisdn": {
                    "description": "MSISDN",
                    "type": "string"
                },
                "time": {
                    "description": "Time",
                    "type": "string"
                },
                "imsi": {
                    "description": "IMSI",
                    "type": "string"
                },
                "iccid": {
                    "description": "ICCID",
                    "type": "string"
                },
                "sequenceNumber": {
                    "description": "The sequence number",
                    "type": "integer",
                    "format": "int64"
                }
            }
        },
        "SubscriptionPatch": {
            "description": "Subscription attributes to be changed",
            "type": "object",
            "properties": {
                "state": {
                    "example": "IN_USE",
                    "description": "The new state of the subscription",
                    "type": "string"
                },
                "msisdn": {
                    "example": "46708421488",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "type": "string"
                },
                "blocked": {
                    "default": false,
                    "description": "If the Subscription is blocked or not",
                    "type": "boolean"
                },
                "odb-profile": {
                    "description": "The new ODB profile",
                    "type": "integer",
                    "format": "int32"
                },
                "iccid": {
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the new SIM to be used for the Subscription",
                    "type": "string"
                }
            }
        },
        "BatchEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about a Batch event",
                    "type": "object",
                    "properties": {
                        "status": {
                            "type": "string"
                        },
                        "batchid": {
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "BatchStatusInfo": {
            "description": "Information about a Batch job",
            "type": "object",
            "properties": {
                "status": {
                    "description": "The status of the batch job",
                    "readOnly": true,
                    "type": "string"
                },
                "creationdate": {
                    "description": "The creation date",
                    "readOnly": true,
                    "type": "string"
                },
                "batchid": {
                    "description": "The ID of this batch",
                    "readOnly": true,
                    "type": "string"
                },
                "requests": {
                    "items": {
                        "$ref": "#/definitions/BatchOrderInfo"
                    },
                    "type": "array"
                }
            }
        },
        "ServicePrototype": {
            "description": "Service to be added",
            "properties": {
                "id": {
                    "description": "Service Id",
                    "type": "string"
                },
                "limit": {
                    "description": "Optional service limit",
                    "type": "integer",
                    "format": "int32"
                },
                "forward-number": {
                    "description": "Optional service forwarding number",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "id"
            ]
        },
        "DiagnosticInfo": {
            "description": "Diagnostic Information",
            "properties": {
                "info": {
                    "description": "Human readable diagnostic information to aid in trouble shooting",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "info"
            ]
        },
        "StateChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about a Threshold event",
                    "type": "object",
                    "properties": {
                        "previous-state": {
                            "description": "Previous state",
                            "readOnly": true,
                            "type": "string"
                        },
                        "new-state": {
                            "description": "New state",
                            "readOnly": true,
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "ThresholdEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about a Threshold event",
                    "type": "object",
                    "properties": {
                        "value": {
                            "description": "Value",
                            "type": "string"
                        },
                        "threshold": {
                            "description": "Threshold",
                            "type": "string"
                        },
                        "service": {
                            "description": "Service name",
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "SubscriptionTypeServiceInfo": {
            "description": "Subscription Type with associated Services",
            "properties": {
                "services": {
                    "items": {
                        "$ref": "#/definitions/ServiceDescription"
                    },
                    "description": "List of available services",
                    "type": "array"
                },
                "name": {
                    "description": "Subscription Type name",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "name",
                "services"
            ]
        },
        "BatchRequestBodyPrototype": {
            "properties": {
                "state": {
                    "example": "IN_USE",
                    "description": "The new state of the subscription",
                    "type": "string"
                },
                "msisdn": {
                    "example": "46708421488",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "type": "string"
                },
                "forward-number": {
                    "description": "Optional service forwarding number",
                    "type": "string"
                },
                "iccid": {
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the new SIM to be used for the Subscription",
                    "type": "string"
                },
                "subscription-type": {
                    "example": "The Holy Subscription",
                    "description": "Subscription type",
                    "type": "string"
                },
                "id": {
                    "description": "Service Id",
                    "type": "string"
                },
                "blocked": {
                    "default": false,
                    "description": "If the Subscription is blocked or not",
                    "type": "boolean"
                },
                "limit": {
                    "description": "Optional service limit",
                    "type": "integer",
                    "format": "int32"
                }
            },
            "type": "object",
            "required": [
                "id",
                "subscription-type"
            ]
        },
        "OrderInfo": {
            "description": "List of order identifiers",
            "properties": {
                "orders": {
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    },
                    "description": "List of order identifiers",
                    "type": "array"
                }
            },
            "type": "object",
            "required": [
                "orders"
            ]
        },
        "ServiceDescription": {
            "description": "Information about a Service",
            "properties": {
                "id": {
                    "description": "The Service identifier",
                    "type": "string"
                },
                "description": {
                    "description": "Optional description",
                    "type": "string"
                }
            },
            "type": "object",
            "required": [
                "id"
            ]
        },
        "OrderEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about an Order event",
                    "type": "object",
                    "properties": {
                        "status": {
                            "description": "Order status",
                            "type": "string"
                        },
                        "orderid": {
                            "description": "Order id",
                            "readOnly": true,
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "NetworkChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "description": "Information about a Network Change event",
                    "type": "object",
                    "properties": {
                        "mnc": {
                            "description": "MNC",
                            "readOnly": true,
                            "type": "string"
                        },
                        "domain": {
                            "description": "Domain",
                            "readOnly": true,
                            "type": "string"
                        },
                        "mcc": {
                            "description": "MCC",
                            "readOnly": true,
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "SubscriptionInfo": {
            "description": "Basic information about a Subscription",
            "properties": {
                "status": {
                    "description": "Subscriber status",
                    "type": "string"
                },
                "msisdn": {
                    "example": "46708421488",
                    "description": "The MSISDN (E.164 number) of the Subscription",
                    "type": "string"
                },
                "iccid": {
                    "example": "89461177710001700003",
                    "description": "The ICCID identifying the SIM used by the Subscription",
                    "type": "string"
                },
                "subscription-type": {
                    "example": "The Holy Subscription",
                    "description": "Subscription type",
                    "readOnly": true,
                    "type": "string"
                },
                "odb-profile": {
                    "example": "1",
                    "description": "ODB profile",
                    "readOnly": true,
                    "type": "string"
                },
                "imsi": {
                    "example": "244141000170000",
                    "items": {
                        "type": "string"
                    },
                    "description": "A list of IMSI numbers used by the Subscription",
                    "type": "array"
                },
                "blocked": {
                    "default": false,
                    "description": "If the Subscriber is blocked or not",
                    "type": "boolean"
                },
                "ongoing-orders": {
                    "example": "10049",
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    },
                    "description": "A list of Order IDs for provisioning orders in progress on the Subscription",
                    "readOnly": true,
                    "type": "array"
                }
            },
            "type": "object",
            "required": [
                "iccid"
            ]
        },
        "BatchPrototype": {
            "description": "Parameters required at creation of a new Batch",
            "type": "object",
            "properties": {
                "requests": {
                    "items": {
                        "$ref": "#/definitions/BatchRequestPrototype"
                    },
                    "description": "List of requests in the batch",
                    "type": "array"
                },
                "type": {
                    "description": "Type of request. Either 'single' or 'multi'",
                    "type": "string"
                }
            }
        }
    },
    "securityDefinitions": {
        "basic_auth": {
            "type": "basic"
        }
    }
}

```

