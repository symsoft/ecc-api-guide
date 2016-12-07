### Get Mobile Network information

Mobile Network information, such as which mobile network a device is attached to can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}/mobile-network_ path.
On succes, the response contains the following information
- **imsi**: current used imsi
- **cs-node**: msc/vlr E.214 global title address
- **ps-node**: sgsn address. E.214 Mobile Global Title or host and realm
- **eps-node**: mme address. E.214 Mobile Global Title or host and realm
- **mcc**: Mobile Country Code
- **mnc**: Mobile Network Code
__Example Command:__
```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488/mobile-network
```

__Example Request:__
```
GET /ecc/v1/subscriptions/msisdn:46708421488/mobile-network HTTP/1.1
Host: 172.16.20.14:8081
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
```

__Example Response:__
```
HTTP/1.1 200 OK
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 09:52:43 GMT
Content-Length: 121

{
  "imsi": "244141000170000"
  "cs-node" : "4828132801",
  "ps-node" : { "number" : "4828130051"},
  "eps-node" : "host" : "mms-1", "realm" : "epc.mnc001.mcc244.3gppnetwork.org"
  "mcc" : "244"
  "mnc": "001"
  ]
}
```
