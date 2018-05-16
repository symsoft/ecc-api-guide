### Change ODB Profile

Change the ODB \(Operator Determined Barring\) profile  of a Subscription by issue a PATCH request on the _/ecc/v1/subscriptions/{type}:{id}_ path. The body of the request shall include the desired ODB profile identifier. The valid set of ODB profile identifiers are defined as part of the onboarding process.

**Example Command:**

```
curl --request PATCH \
 --data '{"odb-profile" : 1}' \
 --header "Content-type: application/json" \
 --header "Accept: application/json" \
 https://user:password@api.ecc.symsoft.com/ecc/v1/subscriptions/msisdn:46708421488
```

**Example Request:**

```
PATCH /ecc/v1/subscriptions/msisdn:46708421488 HTTP/1.1
Host: api.ecc.symsoft.com
Authorization: Basic c3VwZXI6c3VwZXI=
User-Agent: curl/7.43.0
Accept: application/json
Content-Type: application/json
Content-Length: 24

{
  "odb-profile" : 1
}
```

**Example Response:**

```
HTTP/1.1 202 Accepted
Server: Nobill/5.3.0
Content-Type: application/json;charset=UTF-8
Date: Thu, 10 Mar 2016 15:39:18 GMT
Content-Length: 26

{
  "orders": [
    20144
  ]
}
```

#### Available ODB profiles

An ODB profile restricts the subscriber possibility to initiate and/or receive calls and SMS when roaming and is managed by the ECC tenant via the ECC API \(see above\).

The ODB profile has the following attributes:

* Id: the identity of the profile used in the ECC API.
* Description: described the ODB profile
* Home country: defines the home country, where the barring shall **not** apply
* Home PLMNId: MCC or MCC/MNC corresponds to home country.
* ODB setting: enabled ODB rules.

The ODB profile applies on all countries/networks **except** the home country/network \(i.e. HPLMN or EHPLMN\)

ECC has implemented the ODB profiles listed in the table below.

| ODB profile id | Slogan | \(E\)HPLMN | ODB description |
| --- | --- | --- | --- |
| 0 | No barring | \* | No barring, services allowed everywhere |
| 1 | Bar Premium calls | \* | Bar Outgoing-premium-rate-calls everywhere |
| 10 | Bar Premium when roaming | 26001 | Bar Outgoing-premium-rate-calls \(info + entertainment\) |
| 11 | Bar all in- \(MTC\) and outgoing call \(MOC\) when roaming | 26001 | Bar in- and outgoing calls |
| 12 | Bar all outgoing call \(MOC\) when roaming | 26001 | Bar all outgoing call \(MOC\) |
| 13 | Bar all incoming call \(MTC\) when roaming | 26001 | Bar all incoming call \(MTC\) |

The profiles 0 and 1 are valid for all networks. Select profile 0 when all voice and sms services are allowed on all networks. Profile 1 will bar premium services in all networks.

