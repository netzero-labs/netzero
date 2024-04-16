# Netzero - Dynamic Electricity Pricing

## Introduction
[Netzero](https://www.netzeroapp.io) is an iOS/Android/web app designed for monitoring
and optimizing your Tesla Solar/Powerwall system. Netzero is adding support for dynamic
electricity pricing (also known as dynamic tariffs, real-time pricing, or wholesale pricing).
These utility plans have pricing that reflects the variation in wholesale electricity costs
due to changes in supply and demand.  The prices change frequently (as frequently as every
30 minutes) and are usually forecast for the next 24 hours.

By shifting usage based on real-time pricing (e.g. reducing usage during expensive peaks),
utility customers can save on electricity costs.  A solar and battery system in combination
with accurate rate plans is a great way to achieve that goal!

## Agile Octopus Pilot

Netzero currently supports [Agile Octopus](https://octopus.energy/smart/agile/) plans from
Octopus Energy.  We will add support for additional plans and utilities in the future, [let
us know](mailto:feedback@netzeroapp.io) if you're currently on a dynamic plan and
would like to participate.

## Configuration

If Octopus Energy is your utility provider, you will see a "Utility Rate Plan" option in the
main menu.  Configure your region, import and export tariff, and check the "Automatically
update rate plan" checkbox.  This will result in a few changes:
- Your prior tariff configuration will be overridden.  In the future, the app will allow
  restoring the original plan; for now, make sure to write down your existing rate plan if
  you created it manually and might need it in the future.
- Your new tariff configuration will reflect the current 24h predicted pricing.
- As new tariffs are announced (usually around 4pm), the tariff configuration will be
  automatically updated.  You do not need to keep the app open for that.

Note that the Tesla app's Utility Rate Plan section doesn't display dynamic tariffs properly:

<img src="utility-rate-plan.png" width="300" alt="Utility Rate Plan" />

We will work with the Tesla team to make sure this gets corrected.  For, you can instead use the=
Buy and Sell charts (shown by scrolling down under the Grid chart) to display the real-time prices:

<img src="buy-sell-prices.png" width="300" alt="Buy and Sell Prices" />

## Disabling Automatic Updates

If you wish to stop updating your dynamic tariffs, uncheck the "Automatically update rate plan"
checkbox under "Utility Rate Plan".  Make sure to also configure a new rate plan using the Tesla app,
using the Start Over function.


## Feedback

Send any questions or comments to [feedback@netzeroapp.io](mailto:feedback@netzeroapp.io).
