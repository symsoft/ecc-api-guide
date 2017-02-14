## API Specification

The formal ECC API specification in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format.

```yaml
---
{
    "swagger": "2.0",
    "info": {
        "description": "Symsoft Enterprise Communications Cloud API",
        "version": "v0.8.2",
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
        "/batches/{batchid}": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "Read Batch",
                "responses": {
                    "404": {
                        "description": "No queue for event type"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/BatchStatusInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "Get batch information.",
                "parameters": [
                    {
                        "required": true,
                        "type": "string",
                        "description": "The batch uuid",
                        "in": "path",
                        "name": "batchid"
                    }
                ],
                "operationId": "getBatch",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Batch"
                ]
            }
        },
        "/events/{event-type}": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "Read Events",
                "responses": {
                    "404": {
                        "description": "No queue for event type"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/EventListInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "List events of a specific type.",
                "parameters": [
                    {
                        "required": true,
                        "type": "string",
                        "description": "The type of event",
                        "in": "path",
                        "name": "event-type"
                    },
                    {
                        "required": false,
                        "type": "integer",
                        "in": "query",
                        "name": "limit",
                        "format": "int32"
                    },
                    {
                        "required": false,
                        "type": "integer",
                        "in": "query",
                        "name": "first-element",
                        "format": "int64"
                    },
                    {
                        "required": false,
                        "type": "integer",
                        "in": "query",
                        "name": "long-polling",
                        "format": "int32"
                    },
                    {
                        "required": false,
                        "type": "string",
                        "in": "header",
                        "name": "If-None-Match"
                    }
                ],
                "operationId": "getEventTypeChange",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Event"
                ]
            }
        },
        "/subscriptions/{type}:{id}": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "List Subscription information",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/SubscriptionInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "List basic Subscription information. For info about assigned Services, use the listServices operation",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    }
                ],
                "operationId": "getSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Subscription"
                ]
            },
            "patch": {
                "produces": [
                    "application/json"
                ],
                "summary": "Update Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "409": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Conflict"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "consumes": [
                    "application/json"
                ],
                "description": "Change one or several Subscription attributes, such as SIM (identified by ICCID), MSISDN or blocking state.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPatch"
                        },
                        "description": "Subscription attributes to be changed",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "updateSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Subscription"
                ]
            },
            "delete": {
                "produces": [
                    "application/json"
                ],
                "summary": "Delete Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "description": "Delete a Subscription and resources held, such as SIM and MSISDN. Assigned Services will also be deleted.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    }
                ],
                "operationId": "deleteSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Subscription"
                ]
            }
        },
        "/subscriptions/{type}:{id}/services/{sid}/{instance}": {
            "delete": {
                "produces": [
                    "application/json"
                ],
                "summary": "Remove a Service Instance from a Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "description": "Remove a specific Service instance from a Subscription.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Service identifier",
                        "in": "path",
                        "name": "sid"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Instance identifier",
                        "in": "path",
                        "name": "instance"
                    }
                ],
                "operationId": "removeOneService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            }
        },
        "/services": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "List Subscription Types and Services available to API user",
                "responses": {
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/SubscriptionTypeServiceInfoList"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "",
                "parameters": [],
                "operationId": "getServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            }
        },
        "/subscriptions/{type}:{id}/services/{sid}": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "List service details for a Subscription",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/SubscriptionServiceInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "List details of a service assigned to a subscription. Services may have optional attributes.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Service identifier",
                        "in": "path",
                        "name": "sid"
                    }
                ],
                "operationId": "getServiceDetails",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            },
            "patch": {
                "produces": [
                    "application/json"
                ],
                "summary": "Modify a Service belonging to a Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "description": "Modify a Service that's assigned to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Service identifier",
                        "in": "path",
                        "name": "sid"
                    },
                    {
                        "required": false,
                        "schema": {
                            "$ref": "#/definitions/ServicePrototypeExternalSid"
                        },
                        "description": "New data for service",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "modifyService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            },
            "post": {
                "produces": [
                    "application/json"
                ],
                "summary": "Assign a Service to a Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "description": "Assign a Service to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Service identifier",
                        "in": "path",
                        "name": "sid"
                    },
                    {
                        "required": false,
                        "schema": {
                            "$ref": "#/definitions/ServicePrototypeExternalSid"
                        },
                        "description": "Service settings",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "addService",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            },
            "delete": {
                "produces": [
                    "application/json"
                ],
                "summary": "Remove a Service from a Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "description": "Remove a Service from a Subscription. All Service instances with the given identifier will be removed.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "Service identifier",
                        "in": "path",
                        "name": "sid"
                    }
                ],
                "operationId": "removeAllServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            }
        },
        "/orders/{id}": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "Find order",
                "responses": {
                    "404": {
                        "description": "Order not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/OrderExtData"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "",
                "parameters": [
                    {
                        "required": true,
                        "description": "ID of order to be fetched",
                        "format": "int32",
                        "name": "id",
                        "type": "integer",
                        "in": "path"
                    }
                ],
                "operationId": "getOrder",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Order"
                ]
            }
        },
        "/batches": {
            "post": {
                "produces": [
                    "application/json"
                ],
                "summary": "Submit Batch",
                "responses": {
                    "404": {
                        "description": "Batch not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/BatchStatusInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "consumes": [
                    "application/json"
                ],
                "description": "Submit batch job.",
                "parameters": [
                    {
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/BatchPrototype"
                        },
                        "description": "Attributes of Subscription to be created",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "createBatch",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Batch"
                ]
            }
        },
        "/subscriptions/{type}:{id}/mobile-network": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "List mobile network information regarding Subscription",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/MobileNetwork"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    }
                ],
                "operationId": "getMobileNetwork",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Mobile Network"
                ]
            }
        },
        "/subscriptions": {
            "post": {
                "produces": [
                    "application/json"
                ],
                "summary": "Create Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "409": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Conflict"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "consumes": [
                    "application/json"
                ],
                "description": "Create a new Subscription and associate with a SIM (identified by ICCID) and an optional MSISDN.",
                "parameters": [
                    {
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/SubscriptionPrototype"
                        },
                        "description": "Attributes of Subscription to be created",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "createSubscription",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Subscription"
                ]
            }
        },
        "/subscriptions/{type}:{id}/services": {
            "get": {
                "produces": [
                    "application/json"
                ],
                "summary": "List Services assigned to Subscription",
                "responses": {
                    "404": {
                        "description": "Subscription not found"
                    },
                    "200": {
                        "schema": {
                            "$ref": "#/definitions/SubscriptionServiceInfo"
                        },
                        "description": "Successful operation"
                    }
                },
                "description": "List Services assigned to Subscription. Services may have optional attributes.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    }
                ],
                "operationId": "listServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            },
            "post": {
                "produces": [
                    "application/json"
                ],
                "summary": "Assign Services to a Subscription",
                "responses": {
                    "204": {
                        "description": "No change needed"
                    },
                    "404": {
                        "description": "Subscription not found"
                    },
                    "400": {
                        "schema": {
                            "$ref": "#/definitions/DiagnosticInfo"
                        },
                        "description": "Bad request"
                    },
                    "202": {
                        "schema": {
                            "$ref": "#/definitions/OrderInfo"
                        },
                        "description": "Request accepted"
                    }
                },
                "consumes": [
                    "application/json"
                ],
                "description": "Assign Services to a Subscription. Specific Services with identifiers and attributes are pre-defined outside this API.",
                "parameters": [
                    {
                        "required": true,
                        "enum": [
                            "msisdn",
                            "imsi",
                            "iccid"
                        ],
                        "description": "The type of identifier used",
                        "name": "type",
                        "type": "string",
                        "in": "path"
                    },
                    {
                        "required": true,
                        "type": "string",
                        "description": "An MSISDN, IMSI or ICCID number identifying the Subscription",
                        "in": "path",
                        "name": "id"
                    },
                    {
                        "required": true,
                        "schema": {
                            "$ref": "#/definitions/ServiceListPrototype"
                        },
                        "description": "List of Services to be added",
                        "in": "body",
                        "name": "body"
                    }
                ],
                "operationId": "addServices",
                "security": [
                    {
                        "basic_auth": []
                    }
                ],
                "tags": [
                    "Service"
                ]
            }
        }
    },
    "definitions": {
        "BatchOrderInfo": {
            "type": "object",
            "description": "Information about an order in a batch job",
            "properties": {
                "status": {
                    "type": "string",
                    "description": "The status of the request",
                    "readOnly": true
                },
                "requestid": {
                    "type": "string",
                    "description": "The ID of the request",
                    "readOnly": true
                },
                "info": {
                    "type": "string",
                    "description": "Optional extra information about the request",
                    "readOnly": true
                },
                "orderid": {
                    "type": "integer",
                    "description": "The order ID of the request",
                    "format": "int32",
                    "readOnly": true
                }
            }
        },
        "ThresholdEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "type": "object",
                    "description": "Information about a Threshold event",
                    "properties": {
                        "service": {
                            "type": "string",
                            "description": "Service name"
                        },
                        "value": {
                            "type": "string",
                            "description": "Value"
                        },
                        "threshold": {
                            "type": "string",
                            "description": "Threshold"
                        }
                    }
                }
            ]
        },
        "MobileNetwork": {
            "type": "object",
            "description": "Mobile network information",
            "properties": {
                "eps-node": {
                    "$ref": "#/definitions/NodeIdentity",
                    "description": "EPS node",
                    "readOnly": true
                },
                "mcc": {
                    "type": "string",
                    "description": "MCC",
                    "readOnly": true
                },
                "ps-node": {
                    "$ref": "#/definitions/NodeIdentity",
                    "description": "PS node",
                    "readOnly": true
                },
                "cs-node": {
                    "type": "string",
                    "description": "CS node",
                    "readOnly": true
                },
                "mnc": {
                    "type": "string",
                    "description": "MNC",
                    "readOnly": true
                },
                "imsi": {
                    "type": "string",
                    "description": "The current IMSI"
                }
            }
        },
        "DeviceChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "type": "object",
                    "description": "Information about a Device Change event",
                    "properties": {}
                }
            ]
        },
        "SubscriptionServiceInfo": {
            "type": "object",
            "required": [
                "services"
            ],
            "description": "Detailed Service information for a Subscription",
            "properties": {
                "services": {
                    "type": "array",
                    "description": "List of assigned services",
                    "items": {
                        "$ref": "#/definitions/ServiceInfo"
                    }
                },
                "iccid": {
                    "type": "string",
                    "description": "Unique SIM identifier, usually printed on the SIM card",
                    "example": "89461177710001700003"
                },
                "msisdn": {
                    "type": "string",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "example": "46708621488"
                }
            }
        },
        "ServicePrototypeExternalSid": {
            "type": "object",
            "description": "Service to be added",
            "properties": {
                "limit": {
                    "type": "integer",
                    "description": "Optional service limit",
                    "format": "int32"
                },
                "forwarding-number": {
                    "type": "string",
                    "description": "Optional service forwarding number"
                }
            }
        },
        "ServiceListPrototype": {
            "type": "object",
            "required": [
                "services"
            ],
            "description": "List of Services",
            "properties": {
                "services": {
                    "type": "array",
                    "description": "List of services",
                    "items": {
                        "$ref": "#/definitions/ServicePrototype"
                    }
                }
            }
        },
        "BatchRequestPrototype": {
            "type": "object",
            "description": "Parameters required at creation of a new Batch request",
            "properties": {
                "requestid": {
                    "type": "string",
                    "description": "The id of the request",
                    "example": "1276322"
                },
                "method": {
                    "type": "string",
                    "description": "The method of the request",
                    "example": "POST"
                },
                "body": {
                    "$ref": "#/definitions/BatchRequestBodyPrototype",
                    "description": "The body of the request"
                },
                "resource": {
                    "type": "string",
                    "description": "The resource of the request",
                    "example": "subscriptions"
                }
            }
        },
        "OrderInfo": {
            "type": "object",
            "required": [
                "orders"
            ],
            "description": "List of order identifiers",
            "properties": {
                "orders": {
                    "type": "array",
                    "description": "List of order identifiers",
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    }
                }
            }
        },
        "SubscriptionPrototype": {
            "type": "object",
            "required": [
                "iccid",
                "subscription-type"
            ],
            "description": "Parameters required at creation of a new Subscription",
            "properties": {
                "subscription-type": {
                    "type": "string",
                    "description": "Subscription type",
                    "example": "The Holy Subscription"
                },
                "iccid": {
                    "type": "string",
                    "description": "The ICCID identifying the SIM to be used for the Subscription",
                    "example": "89461177710001700003"
                },
                "odb-profile": {
                    "type": "integer",
                    "description": "The new ODB profile",
                    "format": "int32",
                    "example": 1
                },
                "msisdn": {
                    "type": "string",
                    "description": "The MSISDN (E.164 number) of the Subscription",
                    "example": "46708421488"
                }
            }
        },
        "ServiceDescription": {
            "type": "object",
            "required": [
                "id"
            ],
            "description": "Information about a Service",
            "properties": {
                "id": {
                    "type": "string",
                    "description": "The Service identifier"
                },
                "description": {
                    "type": "string",
                    "description": "Optional description"
                }
            }
        },
        "NodeIdentity": {
            "type": "object",
            "description": "Node identity",
            "properties": {
                "number": {
                    "type": "string",
                    "description": "Optional instance identifier"
                },
                "realm": {
                    "type": "string",
                    "description": "Optional instance identifier"
                },
                "host": {
                    "type": "string",
                    "description": "Optional instance identifier"
                }
            }
        },
        "BatchRequestBodyPrototype": {
            "type": "object",
            "required": [
                "id",
                "subscription-type"
            ],
            "properties": {
                "id": {
                    "type": "string",
                    "description": "Service Id"
                },
                "limit": {
                    "type": "integer",
                    "description": "Optional service limit",
                    "format": "int32"
                },
                "forward-number": {
                    "type": "string",
                    "description": "Optional service forwarding number"
                },
                "blocked": {
                    "type": "boolean",
                    "description": "If the Subscription is blocked or not"
                },
                "subscription-type": {
                    "type": "string",
                    "description": "Subscription type",
                    "example": "The Holy Subscription"
                },
                "state": {
                    "type": "string",
                    "description": "The new state of the subscription",
                    "example": "IN_USE"
                },
                "iccid": {
                    "type": "string",
                    "description": "The ICCID identifying the new SIM to be used for the Subscription",
                    "example": "89461177710001700003"
                },
                "msisdn": {
                    "type": "string",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "example": "46708421488"
                }
            }
        },
        "BatchStatusInfo": {
            "type": "object",
            "description": "Information about a Batch job",
            "properties": {
                "batchid": {
                    "type": "string",
                    "description": "The ID of this batch",
                    "readOnly": true
                },
                "creationdate": {
                    "type": "string",
                    "description": "The creation date",
                    "readOnly": true
                },
                "requests": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/BatchOrderInfo"
                    }
                },
                "status": {
                    "type": "string",
                    "description": "The status of the batch job",
                    "readOnly": true
                }
            }
        },
        "ServiceInstanceInfo": {
            "type": "object",
            "required": [
                "instance"
            ],
            "description": "Information about a Subscriber Service instance",
            "properties": {
                "value": {
                    "type": "integer",
                    "description": "Optional value for consuming Service",
                    "format": "int64"
                },
                "instance": {
                    "type": "string",
                    "description": "Instance identifier"
                },
                "expires": {
                    "type": "string",
                    "description": "Optional expiry date of the Service"
                },
                "limit": {
                    "type": "integer",
                    "description": "Optional max value for the consuming Service",
                    "format": "int64"
                }
            }
        },
        "OrderExtData": {
            "type": "object",
            "properties": {
                "completion-date": {
                    "type": "string",
                    "readOnly": true
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
                "iccid": {
                    "type": "string"
                },
                "msisdn": {
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
                    "type": "object",
                    "description": "Information about a Batch event",
                    "properties": {
                        "batchid": {
                            "type": "string"
                        },
                        "status": {
                            "type": "string"
                        }
                    }
                }
            ]
        },
        "EventInfo": {
            "type": "object",
            "description": "Information about an Event",
            "properties": {
                "iccid": {
                    "type": "string",
                    "description": "ICCID"
                },
                "msisdn": {
                    "type": "string",
                    "description": "MSISDN"
                },
                "sequenceNumber": {
                    "type": "integer",
                    "description": "The sequence number",
                    "format": "int64"
                },
                "imsi": {
                    "type": "string",
                    "description": "IMSI"
                },
                "time": {
                    "type": "string",
                    "description": "Time"
                }
            }
        },
        "SubscriptionTypeServiceInfoList": {
            "type": "object",
            "description": "Subscription Type with associated Services",
            "properties": {
                "api-user": {
                    "type": "string",
                    "description": "API user identifier",
                    "readOnly": true
                },
                "subscription-types": {
                    "type": "array",
                    "description": "List of available subscription types with services",
                    "readOnly": true,
                    "items": {
                        "$ref": "#/definitions/SubscriptionTypeServiceInfo"
                    }
                }
            }
        },
        "EventListInfo": {
            "type": "object",
            "required": [
                "events"
            ],
            "description": "Events for a specific event type",
            "properties": {
                "events": {
                    "type": "array",
                    "description": "List of events",
                    "items": {
                        "$ref": "#/definitions/EventInfo"
                    }
                }
            }
        },
        "SubscriptionPatch": {
            "type": "object",
            "description": "Subscription attributes to be changed",
            "properties": {
                "state": {
                    "type": "string",
                    "description": "The new state of the subscription",
                    "example": "IN_USE"
                },
                "iccid": {
                    "type": "string",
                    "description": "The ICCID identifying the new SIM to be used for the Subscription",
                    "example": "89461177710001700003"
                },
                "blocked": {
                    "type": "boolean",
                    "description": "If the Subscription is blocked or not"
                },
                "odb-profile": {
                    "type": "integer",
                    "description": "The new ODB profile",
                    "format": "int32",
                    "example": 1
                },
                "msisdn": {
                    "type": "string",
                    "description": "The new MSISDN (E.164 number) of the Subscription",
                    "example": "46708421488"
                }
            }
        },
        "ServicePrototype": {
            "type": "object",
            "required": [
                "id"
            ],
            "description": "Service to be added",
            "properties": {
                "id": {
                    "type": "string",
                    "description": "Service Id"
                },
                "limit": {
                    "type": "integer",
                    "description": "Optional service limit",
                    "format": "int32"
                },
                "forward-number": {
                    "type": "string",
                    "description": "Optional service forwarding number"
                }
            }
        },
        "StateChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "type": "object",
                    "description": "Information about a Threshold event",
                    "properties": {
                        "new-state": {
                            "type": "string",
                            "description": "New state",
                            "readOnly": true
                        },
                        "previous-state": {
                            "type": "string",
                            "description": "Previous state",
                            "readOnly": true
                        }
                    }
                }
            ]
        },
        "BatchPrototype": {
            "type": "object",
            "description": "Parameters required at creation of a new Batch",
            "properties": {
                "type": {
                    "type": "string",
                    "enum": [
                        "single",
                        "multi"
                    ],
                    "description": "Type of request."
                },
                "requests": {
                    "type": "array",
                    "description": "List of requests in the batch",
                    "items": {
                        "$ref": "#/definitions/BatchRequestPrototype"
                    }
                }
            }
        },
        "DiagnosticInfo": {
            "type": "object",
            "required": [
                "info"
            ],
            "description": "Diagnostic Information",
            "properties": {
                "info": {
                    "type": "string",
                    "description": "Human readable diagnostic information to aid in trouble shooting"
                }
            }
        },
        "OrderEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "type": "object",
                    "description": "Information about an Order event",
                    "properties": {
                        "status": {
                            "type": "string",
                            "description": "Order status"
                        },
                        "orderid": {
                            "type": "string",
                            "description": "Order id",
                            "readOnly": true
                        }
                    }
                }
            ]
        },
        "ServiceInfo": {
            "type": "object",
            "required": [
                "id"
            ],
            "description": "Information about a Subscriber Service instance",
            "properties": {
                "id": {
                    "type": "string",
                    "description": "The Service identifier"
                },
                "limit": {
                    "type": "integer",
                    "description": "Optional max value for the consuming Service",
                    "format": "int64"
                },
                "instance": {
                    "type": "array",
                    "description": "Optional instances",
                    "items": {
                        "$ref": "#/definitions/ServiceInstanceInfo"
                    }
                },
                "reset-date": {
                    "type": "string",
                    "description": "Optional reset date of the Service",
                    "readOnly": true
                },
                "expires": {
                    "type": "string",
                    "description": "Optional expiry date of the Service"
                },
                "value": {
                    "type": "integer",
                    "description": "Optional value for consuming Service",
                    "format": "int64"
                }
            }
        },
        "NetworkChangeEventInfo": {
            "allOf": [
                {
                    "$ref": "#/definitions/EventInfo"
                },
                {
                    "type": "object",
                    "description": "Information about a Network Change event",
                    "properties": {
                        "mcc": {
                            "type": "string",
                            "description": "MCC",
                            "readOnly": true
                        },
                        "mnc": {
                            "type": "string",
                            "description": "MNC",
                            "readOnly": true
                        },
                        "domain": {
                            "type": "string",
                            "description": "Domain",
                            "readOnly": true
                        }
                    }
                }
            ]
        },
        "SubscriptionInfo": {
            "type": "object",
            "required": [
                "iccid"
            ],
            "description": "Basic information about a Subscription",
            "properties": {
                "ongoing-orders": {
                    "type": "array",
                    "items": {
                        "type": "integer",
                        "format": "int32"
                    },
                    "description": "A list of Order IDs for provisioning orders in progress on the Subscription",
                    "example": "10049",
                    "readOnly": true
                },
                "status": {
                    "type": "string",
                    "description": "Subscriber status"
                },
                "blocked": {
                    "type": "boolean",
                    "description": "If the Subscriber is blocked or not"
                },
                "subscription-type": {
                    "type": "string",
                    "description": "Subscription type",
                    "example": "The Holy Subscription",
                    "readOnly": true
                },
                "odb-profile": {
                    "type": "integer",
                    "readOnly": true,
                    "description": "ODB profile",
                    "format": "int32",
                    "example": 1
                },
                "iccid": {
                    "type": "string",
                    "description": "The ICCID identifying the SIM used by the Subscription",
                    "example": "89461177710001700003"
                },
                "imsi": {
                    "type": "array",
                    "description": "A list of IMSI numbers used by the Subscription",
                    "example": "244141000170000",
                    "items": {
                        "type": "string"
                    }
                },
                "msisdn": {
                    "type": "string",
                    "description": "The MSISDN (E.164 number) of the Subscription",
                    "example": "46708421488"
                }
            }
        },
        "SubscriptionTypeServiceInfo": {
            "type": "object",
            "required": [
                "name",
                "services"
            ],
            "description": "Subscription Type with associated Services",
            "properties": {
                "services": {
                    "type": "array",
                    "description": "List of available services",
                    "items": {
                        "$ref": "#/definitions/ServiceDescription"
                    }
                },
                "name": {
                    "type": "string",
                    "description": "Subscription Type name"
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

