### Parameters

Some API parameters occur more frequently and deserves a more verbal explanation.

---

#### msisdn

MSISDN is a number uniquely identifying a subscription in a GSM or a UMTS mobile network. Simply put, it is the telephone number to the SIM card in a mobile/cellular phone. This abbreviation has a several interpretations, the most common one being "Mobile Station International Subscriber Directory Number".

The MSISDN together with IMSI are two important numbers used for identifying a mobile subscriber. The latter is stored in the SIM, i.e. the card inserted into the mobile phone, and each IMSI uniquely identifies the mobile station, its home wireless network, and the home country of the home wireless network, while the former is the number used for routing calls to the subscriber. IMSI is often used as a key in the HLR ("subscriber database") and MSISDN is the number normally dialed to connect a call to the mobile phone.

The MSISDN follows the numbering plan defined in the ITU-T recommendation E.164.

---

#### iccid

Each SIM is internationally identified by its integrated circuit card identifier (ICCID). ICCIDs are stored in the SIM cards and are also engraved or printed on the SIM card body during a process called personalisation. The ICCID is defined by the ITU-T recommendation E.118 as the Primary Account Number. Its layout is based on ISO/IEC 7812. According to E.118, the number is up to 22 digits long, including a single check digit calculated using the Luhn algorithm.

---

#### sid

The Service Identifier is a string that uniquely identifies one of the Services possible to assign to Subscriptions created by the API User.

Each API User has a user specific set of Services. This set of Services is defined and set up during the [onboarding](onboarding.md) procedure.