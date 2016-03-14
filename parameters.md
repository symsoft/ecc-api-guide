### Parameters

Some API parameters occur more frequently and deserves a more verbal explanation.

---

#### msisdn

__TODO__ [E.164](https://en.wikipedia.org/wiki/E.164) number

---

#### iccid

__TODO__ [E.118](https://en.wikipedia.org/wiki/Subscriber_identity_module#ICCID) number

Each SIM is internationally identified by its integrated circuit card identifier (ICCID). ICCIDs are stored in the SIM cards and are also engraved or printed on the SIM card body during a process called personalisation. The ICCID is defined by the ITU-T recommendation E.118 as the Primary Account Number. Its layout is based on ISO/IEC 7812. According to E.118, the number is up to 22 digits long, including a single check digit calculated using the Luhn algorithm.

---

#### sid

The Service Identifier is a string that uniquely identifies one of the Services possible to assign to Subscriptions created by the API user.

Each API user has a user specific set of services. This set of Services is defined and set up during the [Onboarding](onboarding.md) process.