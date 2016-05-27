### Get Mobile Network information

Mobile Network information, such as which mobile network a device is attached to can be retrieved by issuing a GET request on the _/ecc/v1/subscriptions/{type}:{id}/mobile_network_ path.


__Example Command:__
```
curl --header "Accept: application/json" \
 https://user:password@172.16.20.14:8081/ecc/v1/subscriptions/msisdn:46708421488/mobile_network
```

__Example Request:__
```
GET /ecc/v1/subscriptions/msisdn:46708421488/mobile_network HTTP/1.1
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
  "ps-node" : "4828130051",
  "eps-node" : "4828130081",
  "mccmnc" : "24401"
  ]
}
```