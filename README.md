# ITE College West Weather & Outdoor Work Dashboard

Version: 1.6.5a RC1

Release Name:
Pilot Release Candidate

## Purpose

This dashboard provides live weather intelligence and outdoor work decision support for ITE College West.

The dashboard consolidates:

- MSS Lightning
- WBGT
- Temperature
- Relative Humidity
- Rainfall
- PSI (West Region)
- 2-Hour Forecast

The objective is to support:

- Outdoor work planning
- Facilities Management operations
- Grounds maintenance
- Sports activities
- Campus events
- Contractor management
- EHS monitoring
- Emergency preparedness

The dashboard is a decision-support tool and does not replace:

- Approved risk assessments
- Work Authorisation controls
- Permit-to-Work requirements
- MSS Lightning Alerts
- Supervisor instructions
- Emergency response procedures

---

# Current Release

Version:
1.6.5a RC1

Release Status:
Pilot Release Candidate

---

# Major Features

## Campus-Aware Data Selection

Reference Location:

ITE College West

Latitude:
1.3764369

Longitude:
103.7523055

The dashboard selects the nearest valid station separately for:

- WBGT
- Temperature
- Humidity
- Rainfall

This prevents loss of data when a station reports one metric but not another.

---

## MSS Lightning Risk Engine

Lightning observations are assessed relative to ITE College West.

Risk Classification:

- RED ≤ 8 km
- AMBER > 8 km and ≤ 15 km
- GREEN > 15 km

Information displayed:

- Nearest observation distance
- Risk category
- Payload validation
- Schema monitoring

---

## WBGT Monitoring

Features:

- Nearest WBGT station selection
- Heat Stress Class
- Station Name
- Station ID
- Distance from campus
- Payload validation

Heat Risk Categories:

- HIGH
- MODERATE
- LOW

---

## Temperature Monitoring

Features:

- Nearest station selection
- Temperature value
- Station distance
- Payload validation

---

## Relative Humidity Monitoring

Features:

- Nearest station selection
- Humidity value
- Station distance
- Payload validation

---

## Rainfall Monitoring

Features:

- Nearest station selection
- Rainfall amount
- Station distance
- Payload validation

---

## PSI Monitoring

Source:

West Region PSI

Classification:

- Good / Moderate
- Unhealthy
- Very Unhealthy
- Hazardous

---

## Forecast Monitoring

Approved campus forecast areas:

Primary:
- Choa Chu Kang

Secondary:
- Tengah

No unrelated forecast area fallback is allowed.

---

# Outdoor Work Advisory Engine

Version 1.6.5a RC1 introduces:

## Primary Hazard

Highest-priority active hazard.

Examples:

- Lightning Within 8 km
- Lightning Within 15 km
- High Heat Stress
- Unhealthy Air Quality
- Rain Detected Near Campus

Each hazard displays:

- Measurement
- Trigger
- Control Basis

---

## Supporting Conditions

Displays up to three additional active conditions.

Examples:

- Heavy Thundery Showers Forecast
- Rain Detected Near Campus
- Moderate Heat Stress

---

## Affected Activities

Examples:

- Work at Height
- Outdoor Events
- Open-Field Activities
- Event Setup
- Strenuous Outdoor Work

---

## Operational Actions

Actions are specific to the currently selected Primary Hazard.

---

## Control Priority

Levels:

- IMMEDIATE ACTION REQUIRED
- HIGH ATTENTION REQUIRED
- CONTROLS REQUIRED
- ROUTINE MONITORING
- DATA VERIFICATION REQUIRED

---

## Decision Basis

Provides quick operational context:

- Lightning
- WBGT
- PSI
- Forecast

Supports:

- Shift handovers
- Incident reviews
- Management reporting
- EHS documentation

---

# Payload Validation

Permanent validation:

- MSS Lightning
- WBGT
- Temperature
- Humidity
- Rainfall

Validation checks:

- Schema structure
- Station availability
- Reading availability
- Station matching
- Coordinate availability
- Distance calculation

---

# Refresh Behaviour

Automatic Refresh:

5 minutes

Manual Refresh:

Refresh Now

Controls:

- Active refresh lock
- Queued refresh protection
- API rate limit handling

---

# Dashboard Health

States:

- INITIALISING
- REFRESHING
- HEALTHY
- DEGRADED

API States:

- OK
- LOADING
- RATE LIMITED
- UNAVAILABLE
- MAPPING UNAVAILABLE

---

# Data Sources

Meteorological Service Singapore (MSS)

National Environment Agency (NEA)

Platform:

data.gov.sg

---

# Release Assessment

Version:
1.6.5a RC1

Assessment:

Pilot Ready

Focus Areas During Pilot:

- Location selection accuracy
- Advisory usefulness
- Control Priority accuracy
- Forecast mapping
- Validation failures
- API behaviour

---

# Maintainer

Kelvin Siow

ITE College West
C&W Services (S) Pte Ltd
