### SIM ordering

The SIM ordering process is a manual process currently not part of the API.

The SIM ordering process uses the SIM profile established during the [onboarding](onboarding.md) process.

As a result of the SIM ordering process the API User will get a set of SIM cards. Each card is identified by a ICCID number. This number is usually printed on the physical card.

Information about the SIM cards are also stored in the ECC platform. The API User will need to indicate what SIM card to use for a specific Subscription by using the _[iccid](parameters.md#iccid)_ parameter at [Subscription creation](create_subscription.md). It is also possible to [change SIM](change_sim.md) in use by a Subscription at a later stage should need arise.

The SIM ordering process may be repeated several times.  
