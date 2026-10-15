# ITE College West Weather & Outdoor Work Dashboard

## Version
**v1.7.0 RC1**

## Purpose
The dashboard provides real-time decision support for outdoor work, PE lessons, grounds maintenance, security operations, campus events and contractor activities at ITE College West.

## Core Functions
- WBGT monitoring
- Lightning monitoring
- PM2.5 monitoring
- PSI monitoring
- Rainfall monitoring
- Temperature monitoring
- Humidity monitoring
- 2-Hour Weather Forecast
- Outdoor Work Advisory Engine
- Risk Matrix

## Data Sources
- Data.gov.sg
- National Environment Agency (NEA)
- Meteorological Service Singapore (MSS)

## APIs
- WBGT
- Lightning
- PSI (24-Hour)
- PM2.5 (1-Hour)
- 2-Hour Forecast
- Air Temperature
- Relative Humidity
- Rainfall

## Air Quality Logic
### PSI
Purpose: Next-day planning.

### PM2.5
Purpose: Immediate outdoor activity decision making.

### PM2.5 Thresholds
| PM2.5 (µg/m³) | Status | Action |
|---|---|---|
| 0-55 | Normal | Normal activities |
| 56-150 | Elevated | Reduce strenuous outdoor activity |
| 151-250 | High | Avoid strenuous outdoor activity |
| ≥251 | Very High | Minimise outdoor activity |

### Air Quality Risk Calculation
The dashboard adopts the more restrictive condition between PSI and PM2.5.

## Lightning Management Logic
### RED
Trigger: Lightning ≤8 km

Actions:
- Stop outdoor activities
- Suspend work at height
- Suspend outdoor sports and events
- Move personnel to shelter

### AMBER
Trigger: Lightning >8 km and ≤15 km

Actions:
- Maintain suspension of exposed activities
- Prepare shelter arrangements
- Continue monitoring

### GREEN
Trigger: No lightning within 15 km

Actions:
- Continue activities under approved controls

## Lightning Clearance Logic (v1.7.0)
### Clearance Start Conditions
A 30-minute clearance countdown starts only after a successful MSS lightning update confirms no lightning within 15 km.

### Countdown Reset Conditions
The countdown is cancelled and restarted when:
- Lightning ≤8 km is detected.
- Lightning >8 km and ≤15 km is detected.

### API Failure Lockout
If lightning data is unavailable:
- Clearance is blocked.
- Activities remain suspended.
- A fresh 30-minute clearance period is required after service recovery.

### Countdown Completion
At 00:00, the dashboard changes to:

**ELIGIBLE FOR RESUMPTION REVIEW**

Activities do not automatically resume.

### Supervisor Confirmation
A supervisor must positively confirm resumption before activities restart.

## Audit Records
The dashboard records:
- Last ≤8 km detection
- Last 8-15 km detection
- Clearance start time
- Latest successful lightning check
- Supervisor confirmation time

## Banner Priority
1. Lightning ≤8 km
2. Lightning suspension / clearance state
3. PM2.5 Very High
4. PSI Very Unhealthy / Hazardous
5. High Heat Stress
6. Forecast / Weather Monitoring

## Disclaimer
Decision-support tool only. Users must follow approved site procedures, risk assessments, official MSS and NEA advisories, and supervisor instructions.

## Author
Kelvin Siow
EHS Manager
ITE College West
C&W Services (S) Pte Ltd
