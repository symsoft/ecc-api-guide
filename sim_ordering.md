### SIM ordering

The SIM ordering procedure is a manual procedure currently not part of the API.

The SIM ordering procedure uses the SIM profile established during the [onboarding](onboarding.md) procedure.

As a result of the SIM ordering procedure the API User will get a set of SIM cards. Each card is identified by a ICCID number. This number is usually printed on the physical card.

Information about the SIM cards are also stored in the ECC platform. The API User will need to indicate what SIM card to use for a specific Subscription by using the _[iccid](parameters.md#iccid)_ parameter at [Subscription creation](create_subscription.md). It is also possible to [change SIM](change_sim.md) in use by a Subscription at a later stage should need arise.

The SIM ordering procedure may be repeated several times as the API User requires additional SIM cards. It is worth to notice that this procedure may involve manufacturing of cards and may thus take some time.  
