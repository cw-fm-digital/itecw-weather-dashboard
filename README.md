# ITE College West Weather Dashboard

A browser-based weather and outdoor-work decision-support dashboard for ITE College West. The dashboard retrieves environmental data from data.gov.sg real-time APIs and presents weather conditions, safety status, data integrity, API health, and operational advisories through GitHub Pages.

## Current Release

- **Version:** 1.5.7
- **Release:** Operational Awareness Enhancement
- **Status:** Deployment candidate
- **Site region:** West
- **Forecast mapping:** Choa Chu Kang, then Tengah
- **Refresh interval:** 5 minutes
- **Display timezone:** Singapore Time

## Purpose

The dashboard supports monitoring and planning for:

- Outdoor maintenance
- Roof work
- Work at height
- Landscaping and external cleaning
- Open-field activities
- Outdoor events and sports
- Contractor work planning
- Weather-related operational reviews

The dashboard is a decision-support display. It does not replace approved risk assessments, work procedures, Work Authorisations, Permits-to-Work, official lightning alerts, emergency plans, or supervisor instructions.

## Key Features

### Live Weather and Environmental Data

- Wet Bulb Globe Temperature (WBGT)
- Heat stress classification
- Singapore-wide lightning observations
- 24-hour PSI for the West region
- Air temperature
- Relative humidity
- Rainfall
- 2-hour weather forecast

### Fixed-Site Data Selection

- PSI fixed to the West region
- Forecast restricted to Choa Chu Kang and Tengah
- No fallback to an unrelated forecast area
- Temperature, humidity, and rainfall selected from the nearest available West-region station
- Station name, station identifier, approximate distance, and region displayed where available

### Safety Decision Support

- Green, Amber, Red, Hazardous, and Unknown states
- Outdoor Work Advisory
- Lightning-specific alert and advisory
- Hazardous air-quality alert and advisory
- Heat stress risk
- Lightning risk
- Air-quality risk
- Weather risk
- Overall risk matrix

### Operational Awareness

- Initialising state
- Refreshing state
- Healthy state
- Degraded state
- API status labels and icons
- Mapping Unavailable forecast status
- Dashboard health summary
- Footer dashboard status
- Manual Refresh Now button
- Last successful update time
- Next scheduled refresh time

### Reliability Controls

- Five-minute automatic refresh
- Staggered API requests
- HTTP 429 rate-limit handling
- Failed-metric cleanup
- Grey unavailable-data indicators
- Live Data Incomplete protection
- Queued refresh protection
- `try/finally` refresh recovery
- Retention of clear API status information
- Manual-refresh locking during an active refresh

## Safety Logic

### Lightning Detected

Triggered when the lightning API returns one or more observation records.

Dashboard response:

- Blinking lightning icon
- Blinking lightning count
- Blinking main banner
- `LIGHTNING DETECTED` banner
- Red overall risk
- Lightning-specific Outdoor Work Advisory

Advisory actions:

- Suspend roof works
- Suspend open-field activities
- Suspend outdoor sports and events
- Move personnel to shelter
- Follow site lightning safety procedures

> **Important:** The lightning count represents Singapore-wide observations returned by the API. It is not distance-filtered for ITE College West and is not a campus-specific lightning warning. Continue to use approved official lightning alerts and site procedures.

### Hazardous Air Quality

Triggered when:

- PSI is above 300

Dashboard response:

- `HAZARDOUS AIR QUALITY` banner
- Hazardous air-quality advisory

Advisory actions:

- Minimise outdoor activity
- Avoid prolonged outdoor exposure
- Review non-essential outdoor work
- Consider indoor alternatives
- Monitor official haze advisories

### Red: Stop Work / Review Activities

Triggered when any of the following applies:

- Lightning observations are greater than 0
- WBGT is 32 degrees Celsius or above
- PSI is above 200

### Amber: Proceed With Controls

Triggered when any of the following applies:

- WBGT is 31 degrees Celsius or above
- PSI is above 100
- Forecast contains rain, shower, or thunder
- Rainfall is above 0 mm

Advisory actions:

- Monitor live conditions
- Apply hydration and rest controls
- Confirm shelter arrangements
- Review planned outdoor activities

### Green: Safe to Proceed

Displayed when no Lightning, Hazardous, Red, Amber, or Unknown condition applies.

Advisory actions:

- Outdoor work may proceed under approved controls
- Continue weather monitoring
- Maintain hydration
- Follow approved risk assessments and work procedures

### Unknown: Live Data Incomplete

Displayed when one or more critical feeds are unavailable and no confirmed Red condition exists.

Critical feeds:

- WBGT
- Lightning
- PSI
- Forecast

Dashboard response:

- `LIVE DATA INCOMPLETE` banner
- Grey unknown-risk indicators
- Warning not to interpret missing data as safe conditions
- Direction to check official weather and lightning information

## Dashboard Health States

| State | Meaning |
|---|---|
| Initialising | First live-data cycle is loading |
| Refreshing | A refresh cycle is in progress |
| Healthy | All configured data sources are available |
| Degraded | One or more data sources are rate limited, unavailable, or not mapped |

## API Health States

| Status | Display | Meaning |
|---|---|---|
| `LOADING` | Refresh icon | Request not completed |
| `OK` | Green check | Data source completed successfully |
| `RATE_LIMITED` | Warning icon | API returned HTTP 429 |
| `MAPPING_UNAVAILABLE` | Warning icon | API responded, but no approved forecast area was returned |
| `UNAVAILABLE` | Cross icon | Network, HTTP, payload, or parsing failure |

## Data Sources

The dashboard uses these data.gov.sg real-time endpoints:

```text
WBGT
https://api-open.data.gov.sg/v2/real-time/api/weather?api=wbgt

Lightning
https://api-open.data.gov.sg/v2/real-time/api/weather?api=lightning

PSI
https://api-open.data.gov.sg/v2/real-time/api/psi

2-Hour Forecast
https://api-open.data.gov.sg/v2/real-time/api/two-hr-forecast

Air Temperature
https://api-open.data.gov.sg/v2/real-time/api/air-temperature

Relative Humidity
https://api-open.data.gov.sg/v2/real-time/api/relative-humidity

Rainfall
https://api-open.data.gov.sg/v2/real-time/api/rainfall
```

## Technology

- HTML5
- CSS3
- JavaScript
- Fetch API
- GitHub Pages
- data.gov.sg real-time APIs

No framework, build tool, server, database, or client-side API key is required for the current release.

## Repository Structure

```text
/
├── index.html
├── README.md
├── CHANGELOG.md
└── RELEASE_NOTES_v1.5.7.md   optional
```

## GitHub Pages Deployment

1. Back up the current production `index.html`.
2. Create a stable branch for the previous release.
3. Upload the v1.5.7 file as `index.html` in the repository root.
4. Commit the update to the deployment branch.
5. Confirm GitHub Pages uses the deployment branch and root folder.
6. Open the published dashboard.
7. Perform a hard refresh.
8. Confirm that all seven API feeds complete one refresh cycle.
9. Confirm that the footer and System Health panel show the expected state.

### Hard Refresh

- Windows Chrome or Edge: `Ctrl + Shift + R` or `Ctrl + F5`
- With Developer Tools open: select **Network**, enable **Disable cache**, and refresh

## Manual Refresh

Select **Refresh Now** to request an immediate refresh.

The control is disabled during an active refresh. If another refresh request occurs during an active cycle, one additional refresh is queued. Multiple repeated requests do not create a refresh storm.

## Test Mode

The script includes controlled test switches:

```javascript
const TEST_MODE = {
    LIGHTNING: false,
    PSI: false,
    WBGT: false,
    RAINFALL: false
};
```

- `false` means live production mode.
- `true` means simulated test mode for that metric.
- Set all switches to `false` before production deployment.

### Lightning Test

```javascript
TEST_MODE.LIGHTNING = true;
```

Expected result:

- Lightning count is simulated
- Lightning icon blinks
- Lightning count blinks
- Main banner blinks
- Overall risk becomes Red
- Lightning-specific advisory appears

Restore:

```javascript
TEST_MODE.LIGHTNING = false;
```

## Deployment Acceptance Checks

Confirm the following after deployment:

- Version label shows `1.5.7`
- Site Region shows `WEST`
- Region selector is not displayed
- WBGT loads
- Lightning loads
- PSI West loads
- Forecast uses Choa Chu Kang or Tengah
- Temperature station metadata loads
- Humidity station metadata loads
- Rainfall station metadata loads
- API health labels are visible
- Dashboard health state is visible
- Manual refresh works
- Last successful update changes after refresh
- Next scheduled refresh is displayed
- No JavaScript syntax error appears in the browser Console

## Known Limitations

- Lightning observations are Singapore-wide and are not distance-filtered for ITE College West.
- The lightning count does not confirm an official campus lightning warning.
- External API availability and rate limits may affect individual readings.
- Station selection depends on the station metadata and data returned by the API.
- Approximate station distance is used for selection and display, not for regulatory or survey purposes.
- Forecast mapping uses only Choa Chu Kang and Tengah. If neither area is returned, the dashboard shows `MAPPING UNAVAILABLE`.
- The dashboard is not the sole basis for starting, continuing, suspending, or resuming work.

## Branch and Release Workflow

Recommended branches:

```text
main            Active deployment or development
stable-v1.5.6   Previous reliability baseline
stable-v1.5.7   Operational Awareness Enhancement baseline
```

Recommended release process:

1. Confirm the live dashboard works.
2. Create a stable branch.
3. Test changes outside the stable branch.
4. Validate API, safety, and health states.
5. Deploy only after acceptance checks pass.
6. Retain the previous stable release for rollback.

## Version Summary

| Version | Focus |
|---|---|
| 0.1 | Static prototype |
| 1.0 | Live WBGT and lightning |
| 1.1 | PSI and forecast integration |
| 1.2 | Safety logic and Outdoor Work Advisory |
| 1.3 | Temperature, humidity, and rainfall |
| 1.4 | Visualisation and rate-limit controls |
| 1.5.3 | Lightning Operations Enhancement |
| 1.5.4 | Data Integrity Enhancement |
| 1.5.5 | Operations Visibility Enhancement |
| 1.5.6 | Reliability Hardening |
| 1.5.7 | Operational Awareness Enhancement |

See [`CHANGELOG.md`](CHANGELOG.md) for detailed changes.

## Operational Disclaimer

This dashboard is a monitoring and decision-support aid. Weather and environmental data may be delayed, unavailable, incomplete, corrected later, or subject to API limitations.

Users remain responsible for applying:

- Approved risk assessments
- Safe work procedures
- Work Authorisations
- Permits-to-Work
- Official lightning alerts
- Heat stress controls
- Haze response measures
- Emergency procedures
- Supervisor and management instructions

## Maintainer

Created and maintained for ITE College West EHS and Facilities Operations.

**Created by Kelvin Siow**
