## Formal specification

The formal ECC API specification in Swagger YAML (ref needed).

```yaml
---
swagger: "2.0"
info:
  description: "Symsoft Enterprise Communications Cloud API"
  version: "v0.3.0"
  title: "ECC API"
  termsOfService: "http://symsoft.com/api-terms/"
  contact:
    email: "info@symsoft.com"
  license:
    name: "Apache 2.0"
    url: "http://www.apache.org/licenses/LICENSE-2.0.html"
basePath: "/ecc/v1"
tags:
- name: "Subscriber"
  description: "Operations related to Subscribers"
- name: "Service"
  description: "Operations related to Services"
paths:
  /subscribers:
    post:
      tags:
      - "Subscriber"
      summary: "Create Subscriber"
      description: "Create a new Subscriber and associate with a SIM (identified by\
        \ ICCID) and an MSISDN."
      operationId: "createSubscriber"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        description: "Attributes of Subscriber to be created"
        required: true
        schema:
          $ref: "#/definitions/SubscriberPrototype"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriberInfo"
        400:
          description: "Missing mandatory parameter, or invalid MSISDN"
        404:
          description: "SIM not found"
        409:
          description: "Some input value (ICCID or MSISDN) is already in use"
      security:
      - basic_auth: []
  /subscribers/{msisdn}:
    get:
      tags:
      - "Subscriber"
      summary: "List Subscriber information"
      description: "List basic Subscriber information. For info about assigned Services,\
        \ use the listServices operation"
      operationId: "getSubscriber"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriberInfo"
        404:
          description: "Subscriber not found"
      security:
      - basic_auth: []
    delete:
      tags:
      - "Subscriber"
      summary: "Delete Subscriber"
      description: "Delete a Subscriber and all resources held, such as SIM and MSISDN.\
        \ Assigned Services will also be deleted."
      operationId: "deleteSubscriber"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      responses:
        204:
          description: "Successful operation"
        404:
          description: "Subscriber not found"
      security:
      - basic_auth: []
    patch:
      tags:
      - "Subscriber"
      summary: "Update Subscriber"
      description: "Change one or several Subscriber attributes, such as SIM (identified\
        \ by ICCID), MSISDN or blocking state."
      operationId: "updateSubscriber"
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      - in: "body"
        name: "body"
        description: "Subscriber attributes to be changed"
        required: true
        schema:
          $ref: "#/definitions/SubscriberPatch"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriberInfo"
        400:
          description: "Invalid new MSISDN"
        404:
          description: "Subscriber or SIM not found"
        409:
          description: "Some input value (ICCID or MSISDN) is already in use"
      security:
      - basic_auth: []
  /subscribers/{msisdn}/services:
    get:
      tags:
      - "Subscriber"
      summary: "List Services assigned to Subscriber"
      description: "List Services assigned to Subscriber. Services may have optional\
        \ attributes."
      operationId: "listServices"
      produces:
      - "application/json"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      responses:
        200:
          description: "Successful operation"
          schema:
            $ref: "#/definitions/SubscriberServiceInfo"
        404:
          description: "Subscriber not found"
      security:
      - basic_auth: []
  /subscribers/{msisdn}/services/{sid}:
    post:
      tags:
      - "Subscriber"
      - "Service"
      summary: "Assign a Service to a Subscriber"
      description: "Assign a Service to a Subscriber. Specific Services with identifiers\
        \ and attributes are pre-defined outside this API."
      operationId: "addService"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      - name: "sid"
        in: "path"
        description: "Service identifier"
        required: true
        type: "string"
      responses:
        400:
          description: "Invalid Service"
        204:
          description: "Successful operation"
        404:
          description: "Subscriber not found"
      security:
      - basic_auth: []
    delete:
      tags:
      - "Subscriber"
      - "Service"
      summary: "Remove a Service from a Subscriber"
      description: "Remove a Service from a Subscriber. All Service instances with\
        \ the given identifier will be removed."
      operationId: "removeService"
      parameters:
      - name: "msisdn"
        in: "path"
        description: "The MSISDN (E.164 number) of the Subscriber"
        required: true
        type: "string"
      - name: "sid"
        in: "path"
        description: "Service identifier"
        required: true
        type: "string"
      responses:
        400:
          description: "Invalid Service"
        204:
          description: "Successful operation"
        404:
          description: "Subscriber not found"
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
  SubscriberPatch:
    type: "object"
    properties:
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the new SIM to be used for the Subscriber"
      msisdn:
        type: "string"
        example: "46708621488"
        description: "The new MSISDN (E.164 number) of the Subscriber"
      blocked:
        type: "boolean"
        description: "If the Subscriber is blocked or not"
        default: false
    description: "Subscriber attributes to be changed"
  SubscriberServiceInfo:
    type: "object"
    required:
    - "msisdn"
    - "services"
    properties:
      msisdn:
        type: "string"
        example: "46708621488"
        description: "The new MSISDN (E.164 number) of the Subscriber"
      services:
        type: "array"
        description: "List of assigned services"
        items:
          $ref: "#/definitions/ServiceInfo"
    description: "Detailed Service information for a Subscriber"
  SubscriberInfo:
    type: "object"
    required:
    - "blocked"
    - "iccid"
    properties:
      msisdn:
        type: "string"
        example: "46708621488"
        description: "The MSISDN (E.164 number) of the Subscriber"
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the SIM used by the Subscriber"
      blocked:
        type: "boolean"
        description: "If the Subscriber is blocked or not"
        default: false
    description: "Basic information about a Subscriber"
  SubscriberPrototype:
    type: "object"
    required:
    - "iccid"
    - "msisdn"
    properties:
      iccid:
        type: "string"
        example: "89461177710001700003"
        description: "The ICCID identifying the SIM to be used for the Subscriber"
      msisdn:
        type: "string"
        example: "46708621488"
        description: "The MSISDN (E.164 number) of the Subscriber"
    description: "Parameters required at creation of a new Subscriber"
```

