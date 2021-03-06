### Get Mobile Network information

Mobile Network information, such as which mobile network a device is attached to can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}/mobile-network_ path.  
On success, the response contains the following information:

* **imsi**: current used imsi
* **cs-node**: msc/vlr E.214 global title address
* **ps-node**: sgsn address. E.214 Mobile Global Title or host and realm
* **eps-node**: mme address. E.214 Mobile Global Title or host and realm
* **mcc**: Mobile Country Code
* **mnc**: Mobile Network Code

The mcc/mnc can be mapped to Country and Operator using e.g. [http://mcc-mnc.com](http://mcc-mnc.com).

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/mobile-network
```

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488/mobile-network HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121

{
  "imsi": "244141000170000",
  "cs-node" : "4828132801",
  "ps-node" : { "number" : "4828130051"},
  "eps-node" : { "host" : "mms-1", "realm" : "epc.mnc001.mcc244.3gppnetwork.org" },
  "mcc" : "244",
  "mnc": "001"
}
```

#### Location Lookup \(Cell-Id\)

The returned Mobile Network information can optionally include the location \(lac and cell-id\) of a device by adding a _include=location_ query parameter to the request. A location lookup will be slower than just returning the basic mobile network information.

Parts of the returned _location_ object can be excluded if the network cannot supply this information. If the network cannot provide a location the returned location object will include an _info_ parameter with further information.

The lac and cell-id can be mapped to a geographical location using e.g. [http://www.opencellid.org.](http://www.opencellid.org)

**Example Command:**

```
curl --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/mobile-network?include=location
```

**Example Request:**

```
GET /ecc/v1/subscriptions/msisdn:46708421488/mobile-network?include=location HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121

{
  "imsi": "244141000170000",
  "cs-node" : "4828132801",
  "ps-node" : { "number" : "4828130051"},
  "eps-node" : { "host" : "mms-1", "realm" : "epc.mnc001.mcc244.3gppnetwork.org" },
  "mcc" : "244",
  "mnc": "001",
  "location" : {
    "lac": "6",
    "cell-id": "23423"
  }
}
```

##### **Example Response \(no location information available\):**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121

{
  "imsi": "244141000170000",
  "cs-node" : "4828132801",
  "ps-node" : { "number" : "4828130051"},
  "eps-node" : { "host" : "mms-1", "realm" : "epc.mnc001.mcc244.3gppnetwork.org" },
  "mcc" : "244",
  "mnc": "001",
  "location" : {
     "info": "'ATI not allowed' from HLR"
  }
}
```

### Cancel Location

Mobile network information can be deleted by issuing a DELETE request on the _/ecc/v1/subscriptions/{type}:{id}/mobile-network_ path. This triggers the HLR/HSS to send a Cancel Location.

The Cancel Location will trigger IMSI detach followed by a IMSI attach on the device.

**Example Command:**

```
curl --request DELETE --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488/mobile-network
```

**Example Request:**

```
DELETE /ecc/v1/subscriptions/msisdn:46708421488/mobile-network HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

**Example Response:**

```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 0
```



