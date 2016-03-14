## API Specification

The formal ECC API specification in [OpenAPI](https://github.com/OAI/OpenAPI-Specification) format (__TODO: ref needed__) format.

```yaml
---
swagger: "2.0"
info:
  description: "Symsoft Enterprise Communications Cloud API"
  version: "v0.4.0"
  title: "ECC API"
  termsOfService: "http://symsoft.com/api-terms/"
  contact:
    email: "info@symsoft.com"
  license:
    name: "Apache 2.0"
    url: "http://www.apache.org/licenses/LICENSE-2.0.html"
basePath: "/ecc/v1"
tags:
- name: "Subscription"
  description: "Operations related to Subscriptions"
- name: "Service"
  description: "Operations related to Services"
paths:
  /subscriptions:
    post:
      tags:
      - "Subscription"
      summary: "Create Subscription"
      description: "Create a new Subscription and associate with a SIM (identified\
        \ by ICCID) and an MSISDN."
      operationId: "create"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        description: "Attributes of Subscription to be created"
        required: true
        schema:
          $ref: "#/definitions/SubscriptionPrototype"
      responses:
        202:
          description: "Request accepted"
        400:
          description: "Missing mandatory parameter, or invalid MSISDN"
        404:
          description: "SIM not found"
        409:
          description: "An input value (ICCID or MSISDN) is already in use"
      security:
      - basic_auth: []
  /subscriptions/{msisdn}:
    get:
      tags:
      - "Subscription"
      summary: "List Subscription information"
      description: "List basic Subscription information. For info about assigned Services,\
        \ use the listServices operation"
      operationId: "read"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriptionInfo"
        404:
          description: "Subscription not found"
      security:
      - basic_auth: []
    delete:
      tags:
      - "Subscription"
      summary: "Delete Subscription"
      description: "Delete a Subscription and resources held, such as SIM and MSISDN.\
        \ Assigned Services will also be deleted."
      operationId: "delete"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      responses:
        202:
          description: "Request accepted"
        404:
          description: "Subscription not found"
      security:
      - basic_auth: []
    patch:
      tags:
      - "Subscription"
      summary: "Update Subscription"
      description: "Change one or several Subscription attributes, such as SIM (identified\
        \ by ICCID), MSISDN or blocking state."
      operationId: "update"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      - in: "body"
        name: "body"
        description: "Subscription attributes to be changed"
        required: true
        schema:
          $ref: "#/definitions/SubscriptionPatch"
      responses:
        202:
          description: "Request accepted"
        400:
          description: "Invalid new MSISDN"
        404:
          description: "Subscription or SIM not found"
        409:
          description: "An input value (ICCID or MSISDN) is already in use"
      security:
      - basic_auth: []
  /subscriptions/{msisdn}/services:
    get:
      tags:
      - "Subscription"
      summary: "List Services assigned to Subscription"
      description: "List Services assigned to Subscription. Services may have optional\
        \ attributes."
      operationId: "list"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriptionServiceInfo"
        404:
          description: "Subscription not found"
      security:
      - basic_auth: []
  /subscriptions/{msisdn}/services/{sid}:
    post:
      tags:
      - "Subscription"
      - "Service"
      summary: "Assign a Service to a Subscription"
      description: "Assign a Service to a Subscription. Specific Services with identifiers\
        \ and attributes are pre-defined outside this API."
      operationId: "add"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      - name: "sid"
        in: "path"
        description: "Service identifier"
        required: true
        type: "string"
      responses:
        202:
          description: "Request accepted"
        400:
          description: "Invalid Service"
        404:
          description: "Subscription not found"
      security:
      - basic_auth: []
    delete:
      tags:
      - "Subscription"
      - "Service"
      summary: "Remove a Service from a Subscription"
      description: "Remove a Service from a Subscription. All Service instances with\
        \ the given identifier will be removed."
      operationId: "remove"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscription"
        required: true
        type: "string"
      - name: "sid"
        in: "path"
        description: "Service identifier"
        required: true
        type: "string"
      responses:
        202:
          description: "Request accepted"
        400:
          description: "Invalid Service"
        404:
          description: "Subscription not found"
      security:
      - basic_auth: []
securityDefinitions:
  basic_auth:
    type: "basic"
definitions:
  ServiceInfo:
    type: "object"
    required:
    - "name"
    properties:
      name:
        type: "string"
        description: "The Service identifier"
      value:
        type: "integer"
        format: "int64"
        description: "Optional value for consuming Service"
      expires:
        type: "string"
        description: "Optional expiry date of the Service"
    description: "Information about a Subscriber Service instance"
  SubscriptionPatch:
    type: "object"
    properties:
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the new SIM to be used for the Subscription"
      msisdn:
        type: "string"
        example: "46708421488"
        description: "The new MSISDN (E.164 number) of the Subscription"
      blocked:
        type: "boolean"
        description: "If the Subscription is blocked or not"
        default: false
    description: "Subscription attributes to be changed"
  SubscriptionPrototype:
    type: "object"
    required:
    - "iccid"
    - "msisdn"
    properties:
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the SIM to be used for the Subscription"
      msisdn:
        type: "string"
        example: "46708421488"
        description: "The MSISDN (E.164 number) of the Subscription"
    description: "Parameters required at creation of a new Subscription"
  SubscriptionInfo:
    type: "object"
    required:
    - "blocked"
    - "iccid"
    properties:
      msisdn:
        type: "string"
        example: "46708421488"
        description: "The MSISDN (E.164 number) of the Subscription"
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the SIM used by the Subscription"
      blocked:
        type: "boolean"
        description: "If the Subscriber is blocked or not"
        default: false
    description: "Basic information about a Subscription"
  SubscriptionServiceInfo:
    type: "object"
    required:
    - "msisdn"
    - "services"
    properties:
      msisdn:
        type: "string"
        example: "46708621488"
        description: "The new MSISDN (E.164 number) of the Subscription"
      services:
        type: "array"
        description: "List of assigned services"
        items:
          $ref: "#/definitions/ServiceInfo"
    description: "Detailed Service information for a Subscription"
```

