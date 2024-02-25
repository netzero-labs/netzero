# Netzero - Powerwall Automation


## Introduction
[Netzero for Tesla](https://www.netzeroapp.io) is an iOS/Android/web app designed for monitoring
and optimizing your Tesla Solar/Powerwall system. Netzero allows you to schedule Powerwall
configuration changes using the app (backup reserve, operational mode, energy exports, and grid
charging).

For more advanced use, the app also offers an API that allows to manage these configuration changes.


## API Token
Begin by logging into your Tesla account using the [Netzero app](https://www.netzeroapp.io). Access your
API token and energy site ID by navigating to the mode menu (first menu in the top-right) and selecting
**Developer Access**. It's important to keep your API token secure, as while it provides access only
to the data displayed here, it does grant the ability to manage Powerwall configuration.


## Automation with IFTTT
You can utilize the API token to automate Powerwall configuration changes through [IFTTT](https://ifttt.com/) (If This, Then That).
For instance, to establish a specific backup reserve percentage daily at a designated time:

1. Visit https://ifttt.com/create or use the IFTTT app.
2. **If This**: "Choose Date & Time", then select "Every day at", specify the desired time, and create the trigger.
3. **Then That**: Search for the "Webhooks" service, and select "Make a web request". Configure the web request as illustrated below.
Substitute `123456` with your energy site ID and `AbCdEf` with your API token, both obtained above.  Replace `60` with your desired
backup reserve percentage.

<img src="ifttt.png" width="300" alt="IFTTT" />

Note: Utilizing Webhooks requires a PRO IFTTT plan (currently $3.49/month). For simpler automation, use the in-app
schedule configuration instead. IFTTT is useful for more complex rules (e.g., incorporating weather or other conditions.

You can modify other parameters in addition to backup reserve percentage, see next section for details.


## Automation with API requests
If you're familiar with running web requests using `curl` or similar tools, you can also manage the
configuration with scripts.

To retrieve the current configuration and live status of the system, substitute `$API_TOKEN` and `$SITE_ID` with your respective values obtained above:

```bash
curl -s -H "Authorization: Bearer $API_TOKEN" https://api.netzeroapp.io/api/v1/$SITE_ID/config

{
  "backup_reserve_percent": 80,
  "operational_mode": "autonomous",
  "energy_exports": "pv_only",
  "grid_charging": true,
  "percentage_charged": 98,
  "grid_status": "Active (on_grid)",

  "live_status": {
    "solar_power": 4140,
    "energy_left": 19538.05263157895,
    "total_pack_energy": 28097,
    "percentage_charged": 69.5378603821723,
    "battery_power": -2520,
    "load_power": 1620,
    "grid_power": 0,
    [...],
    "wall_connectors": [
      {
        "din": "1457768-02-G--B7S12345J12345",
        "wall_connector_state": 2,
        "wall_connector_fault_state": 2,
        "wall_connector_power": 0
      }
    ]
  }
}
```

This response includes both configuration values and the current power draw.  If you have a Wall Connector connected to your account, you'll also
see car charging status.

To modify the configuration, send a POST request with new values. You can adjust one or more of the following parameters in the same request:

- `backup_reserve_percent`: Integer values ranging from `0` to `100`.
- `operational_mode`: Select one of:
  - `autonomous` (Time-Based Control, using stored energy to maximize savings based on your utility rate plan),
  - `self_consumption` (Self-Powered, using stored energy to power your home after the sun goes down).
- `energy_exports`: Selec one of:
  - `pv_only` (export solar energy only),
  - `battery_ok` (export both solar energy and stored Powerwall energy),
  - `never` (no export).
- `grid_charging`: Select either `true` or `false`.

You can modify one or more of these values in the same request.

```bash
curl -s -H "Authorization: Bearer $API_TOKEN" -H "Content-Type: application/json" \
    --data '{"backup_reserve_percent": 50, "operational_mode": "self_consumption"}' \
    https://api.netzeroapp.io/api/v1/$SITE_ID/config

{
  "backup_reserve_percent": 50,
  "operational_mode": "self_consumption",
  "energy_exports": "pv_only",
  "grid_charging": true,
  "percentage_charged": 98,
  "grid_status": "Active (on_grid)",
  "live_status": {...}
}
```

The response mirrors that of the GET request, providing the updated configuration (inclusive of any changes made) along with the live status.

## Questions or Issues
You can submit issues or post questions here: [Netzero Issues](https://github.com/netzero-labs/netzero/issues).
