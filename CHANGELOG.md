# Changelog

---

# Version 1.6.5a RC1

Release Name:
Pilot Release Candidate

Release Date:
September 2026

Status:
Pilot Ready

---

## Added

### Primary Hazard Engine

Introduced operational hazard prioritisation.

Primary hazards include:

- Lightning Within 8 km
- Lightning Within 15 km
- High Heat Stress
- Moderate Heat Stress
- Air Quality Events
- Rain Detected
- Wet Weather Forecast
- Live Data Incomplete

---

### Supporting Conditions

Added secondary condition visibility.

Displays:

- Additional hazards
- Forecast conditions
- Rain conditions
- Air quality conditions

Maximum displayed:

3

---

### Affected Activities

Added operational impact section.

Examples:

- Work at Height
- Outdoor Events
- Open-Field Activities
- Event Setup
- Strenuous Outdoor Work

---

### Decision Basis

Added operational evidence panel.

Displays:

- Lightning distance
- WBGT
- PSI West
- Forecast

Supports:

- Incident documentation
- Shift handovers
- Management reviews

---

### Enhanced Trigger Visibility

Primary Hazard now displays:

Measurement

Trigger

Control

Example:

Lightning Within 8 km

Measurement:
0.6 km

Trigger:
Distance ≤ 8.0 km

Control:
Immediate Lightning Control

---

## Changed

### Advisory Engine

Old:

Cause-Based Advisory

New:

Hazard and Control Priority Engine

---

### Lightning Terminology

Removed:

Lightning Near Campus

Lightning Approaching Campus

Added:

Lightning Within 8 km

Lightning Within 15 km

---

### Forecast Terminology

Removed:

Wet Weather Forecast

Added:

Actual forecast label

Examples:

Heavy Thundery Showers Forecast

Showers Forecast

Light Rain Forecast

---

### Control Priority Labels

Old:

IMMEDIATE

HIGH

MEDIUM

ROUTINE

DATA CHECK

New:

IMMEDIATE ACTION REQUIRED

HIGH ATTENTION REQUIRED

CONTROLS REQUIRED

ROUTINE MONITORING

DATA VERIFICATION REQUIRED

---

## Retained

### MSS Lightning Engine

- Location-based assessment
- Distance calculation
- Payload validation
- Schema monitoring

---

### WBGT Engine

- Nearest station selection
- Validation
- Station distance calculation

---

### Campus-Based Station Selection

Retained:

- Temperature
- Humidity
- Rainfall

---

### Forecast Mapping

Retained:

- Choa Chu Kang
- Tengah

No unrelated forecast-area fallback.

---

### Validation Framework

Retained:

- WBGT Validation
- Lightning Validation
- Temperature Validation
- Humidity Validation
- Rainfall Validation

---

# Release Readiness

Critical Bugs:
0

Major Bugs:
0

Minor Issues:
2

Production Impact:
None

Assessment:

Pilot Ready

Confidence:

98%

---

# Previous Releases

1.6.5a
Advisory Wording Refinement

1.6.5
Hazard and Control Priority Engine

1.6.4
Cause-Based Advisory Engine

1.6.3
Campus-Specific Weather Station Selection

1.6.2
Nearest WBGT Station Selection

1.6.1
WBGT Payload Validation

1.6.0
MSS Location-Based Lightning Risk


All notable changes to the ITE College West Weather Dashboard are recorded in this file.

## [1.5.7] - Operational Awareness Enhancement

### Added

- Explicit API health labels and icons
- `MAPPING_UNAVAILABLE` forecast health status
- Dashboard health states for Initialising, Refreshing, Healthy, and Degraded
- Footer Dashboard Status summary
- Fixed Site Region display for West
- Manual `Refresh Now` button
- Manual-refresh locking during an active refresh
- Fixed-site weather-station metadata
- Station name display
- Station identifier display
- Approximate station distance display
- Station region display
- Data-scope legend

### Improved

- Forecast mapping restricted to Choa Chu Kang and Tengah
- Forecast failures now distinguish mapping issues from API failures
- Dashboard Health now reports active refresh cycles as Refreshing
- Footer health status updates with dashboard state
- Temperature, humidity, and rainfall use the nearest available West-region station
- Lightning description states that observations are Singapore-wide and not distance-filtered
- Fixed-site dashboard identity retained while operational-health features were aligned from the Singapore Weather Dashboard

### Removed

- Singapore regional selector
- Preferred-region local storage
- Multi-region operating controls
- Fallback to unrelated forecast areas

### Retained

- Lightning-specific blinking alert
- Hazardous PSI advisory
- Revised PSI thresholds
- Green, Amber, Red, Hazardous, and Unknown safety states
- Live Data Incomplete protection
- Failed-metric cleanup
- Grey unavailable-data indicators
- Queued refresh protection
- `try/finally` refresh recovery
- Five-minute refresh interval
- Test-mode controls

### Validation

- JavaScript syntax check passed
- Region-selector references removed
- Preferred-region storage references removed
- Fixed West configuration confirmed
- Approved forecast fallback list confirmed
- Manual refresh control confirmed

---

## [1.5.6] - Reliability Hardening

### Added

- `try/finally` protection around the full refresh cycle
- Forecast location integrity protection

### Improved

- Refresh state is released after unexpected errors
- A queued refresh can run after the active refresh finishes
- Forecast selection limited to Choa Chu Kang and Tengah
- Forecast card shows unavailable when neither approved area is returned

### Fixed

- Risk of refresh lock-up after an unexpected exception
- Risk of showing a forecast from an unrelated area

---

## [1.5.5] - Operations Visibility Enhancement

### Added

- Initialising Live Data screen
- API Health Monitor
- API loading, success, rate-limited, and unavailable states
- Dashboard Health Summary
- Data-source availability count
- Initial health rendering
- Last Refresh display in Dashboard Health

### Improved

- Startup behaviour
- Troubleshooting visibility
- Unattended display monitoring
- Synchronisation between Last Successful Update and Dashboard Health Last Refresh

---

## [1.5.4] - Data Integrity Enhancement

### Added

- Unknown overall-risk state
- Live Data Incomplete banner
- Failed API cleanup engine
- Grey reset for failed metric values
- Individual Unknown risk colours
- Queued refresh protection using `pendingRefresh`

### Improved

- Missing critical data cannot produce a Green overall result
- Stale values are cleared after failed or rate-limited API calls
- Lightning blinking is removed when lightning data becomes unavailable
- Risk Matrix unknown states display in grey
- Refresh requests received during an active refresh are queued

---

## [1.5.3] - Lightning Operations Enhancement

### Added

- Dedicated Lightning Detected banner
- Blinking lightning icon
- Blinking lightning count
- Blinking main lightning banner
- Lightning-specific Outdoor Work Advisory
- Structured test-mode controls
- Dedicated Hazardous Air Quality banner

### Improved

- Lightning receives the highest alert priority
- PSI classifications aligned to the adopted operational bands
- Risk Matrix air-quality colour mapping
- Advisory wording for lightning and hazardous haze conditions

---

## [1.5.2] - Lightning Alert Visualisation

### Added

- Lightning blink animation
- Automatic blinking removal when observation count returns to zero

### Improved

- Visibility of active lightning observations on control-room and operations displays

---

## [1.5.1] - PSI and Advisory Refinement

### Added

- Hazardous PSI state above 300
- Hazardous air-quality advisory

### Improved

- PSI card labels
- Air-quality risk colours
- Banner condition priority
- Footer HTML structure

### Fixed

- Red PSI threshold changed from above 100 to above 200
- Air Risk Matrix mapping for Unhealthy, Very Unhealthy, and Hazardous states

---

## [1.5.0] - PSI Threshold Alignment

### Changed

- PSI 0 to 100 treated as Good or Moderate
- PSI 101 to 200 treated as Unhealthy and Amber
- PSI 201 to 300 treated as Very Unhealthy and Red
- PSI above 300 treated as Hazardous

### Fixed

- PSI values from 51 to 100 no longer trigger Amber by themselves

---

## [1.4.0] - Weather Visualisation and Reliability

### Added

- Forecast weather icons
- KPI colour bands
- Executive summary strip
- Risk Matrix
- System status display
- Last successful update time
- Next scheduled refresh time
- Responsive layout
- Operational disclaimer

### Improved

- Five-minute refresh interval
- Staggered API requests
- Per-card API failure handling
- Singapore-time formatting
- Mobile display

### Fixed

- Repeated HTTP 429 issues caused by simultaneous requests
- Dashboard stability when one supporting data source is unavailable

---

## [1.3.0] - Extended Weather Module

### Added

- Air temperature
- Relative humidity
- Rainfall
- HTTP 429 handling
- `API Busy` and `N/A` fallback messages

### Fixed

- Temperature JSON mapping
- Humidity JSON mapping
- Rainfall JSON mapping

---

## [1.2.0] - Safety Logic Engine

### Added

- Green, Amber, and Red status banner
- Outdoor Work Advisory card
- Forecast-based warning logic
- Action-focused outdoor-work messages

### Fixed

- Safety banner update sequence
- Missing Outdoor Work Advisory card
- Browser-cache troubleshooting for GitHub Pages deployment

---

## [1.1.0] - PSI and Forecast Integration

### Added

- 24-hour PSI for the West region
- 2-hour weather forecast
- Choa Chu Kang forecast selection
- Tengah forecast fallback

### Fixed

- PSI showing `undefined`
- PSI mapping changed to the West region value
- Forecast JSON mapping
- Forecast card remaining at Loading
- Duplicate braces and catch blocks causing JavaScript syntax errors

---

## [1.0.0] - Live Weather Core

### Added

- Live WBGT
- Heat stress classification
- Live lightning observations
- Automatic refresh
- Live clock and update timestamp

### Fixed

- Initial API integration
- WBGT JSON parsing
- Lightning JSON parsing
- JavaScript startup issues

---

## [0.1.0] - Initial Prototype

### Added

- Static HTML layout
- Weather card framework
- Manual placeholder values
- Initial GitHub Pages deployment

### Known Limitations

- No live weather data
- No safety logic
- No forecast integration
- No API failure handling
