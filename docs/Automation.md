# Netzero API Automation HOWTO

## Introduction
[Netzero for Tesla](https://www.netzeroapp.io) is an iOS/Android/web app for monitoring and optimizing your Tesla Solar/Powerwall system.
Netzero has an API to configure your Powerwall system: manage configuration changes such as backup reserve, operational mode, energy exports, and grid charging.

## API Token
Start by logging in to your Tesla account with the web app at https://app.netzeroapp.io.
In the user menu (top right) there is a Developer Access option.  Copy your API token and energy site id from here.  Note: keep your API token safe -- while the
token doesn't give access to any data other than what is shown here, it does allow one to manage Powerwall configuration.

## Automation with API requests
Note: if you're not comfortable running web requests with `curl` or similar tools, you can skip to the next section for no-code automation with IFTTT.

To get the current configuration (replace `API-TOKEN` and `SITE-ID` with your values from above):
```bash
curl -s -H "Authorization: Bearer $API_TOKEN" https://api.netzeroapp.io/api/v1/$SITE_ID/config
{
  "backup_reserve_percent": 80,
  "operational_mode": "autonomous",
  "energy_exports": "pv_only",
  "grid_charging": true,
  "percentage_charged": 98,
  "grid_status": "Active"
}
```

To modify configuration, send a POST request with new values.  The values that can be modified are:
- `backup_reserve_percent`: integer values from 0 to 100
- `operational_mode`: `autonomous` or `self_consumption`
- `energy_exports`: `pv_only`, `battery_ok`, or `never`
- `grid_charging`: `true` or `false`

You can modify one or more of these values in the same request.

```bash
curl -s -H "Authorization: Bearer $API_TOKEN" -H "Content-Type: application/json" \
    --data '{"backup_reserve_percent": 30, "operational_mode": "self_consumption"}' \
    https://api.netzeroapp.io/api/v1/$SITE_ID/config
{
  "backup_reserve_percent": 30,
  "operational_mode": "self_consumption",
  "energy_exports": "pv_only",
  "grid_charging": true,
  "percentage_charged": 98,
  "grid_status": "Active"
}
```
The response is similar to the GET request: the current configuration (now including changed values) and status of the Powerwall.

## Automation with IFTTT

TBD
