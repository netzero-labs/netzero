# Netzero - Enphase Battery Automation


## Introduction
[Netzero](https://www.netzeroapp.io) is an iOS/Android/web app designed for monitoring
and optimizing your Enphase solar/battery system. Netzero allows you to schedule battery
configuration changes using the app (backup reserve, operational mode, energy exports, and grid
charging).

For more advanced use, the app also offers an API that allows to manage these configuration changes.


## API Token
Begin by logging into your Tesla account using the [Netzero app](https://www.netzeroapp.io). Access your
API token and system ID by navigating to the mode menu (first menu in the top-right) and selecting
**Developer Access**. It's important to keep your API token secure, as while it provides access only
to the data displayed here, it does grant the ability to manage battery configuration.


## Automation with IFTTT
You can utilize the API token to automate battery configuration changes through [IFTTT](https://ifttt.com/) (If This, Then That).
For instance, to establish a specific backup reserve percentage daily at a designated time:

1. Visit https://ifttt.com/create or use the IFTTT app.
2. **If This**: "Choose Date & Time", then select "Every day at", specify the desired time, and create the trigger.
3. **Then That**: Search for the "Webhooks" service, and select "Make a web request". Configure the web request as illustrated below.
Substitute `123456` with your energy site ID and `AbCdEf` with your API token, both obtained above.  Replace `60` with your desired
backup reserve percentage.

<img src="../ifttt.png" width="300" alt="IFTTT" />

Note: Utilizing Webhooks requires a PRO IFTTT plan (currently $3.49/month). For simpler automation, use the in-app
schedule configuration instead. IFTTT is useful for more complex rules (e.g. incorporating weather or other conditions).

You can modify other parameters in addition to backup reserve percentage, see next section for details.


## Automation with API requests
TODO

## Questions or Issues
You can submit issues or post questions here: [Netzero Issues](https://github.com/netzero-labs/netzero/issues).
