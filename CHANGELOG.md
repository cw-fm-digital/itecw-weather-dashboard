# CHANGELOG

## v1.7.0 RC1

### Major Enhancements
- Added corrected lightning clearance state machine.
- Added PM2.5 monitoring integration.
- Added operational lightning action messaging.
- Added supervisor-controlled activity resumption.
- Added lightning audit trail.

### Lightning Logic Improvements
- Lightning ≤8 km triggers STOP OUTDOOR ACTIVITIES.
- Lightning >8 km to ≤15 km maintains suspension state.
- Clearance starts only after successful confirmation of no lightning within 15 km.
- Any lightning within 15 km resets clearance.
- Lightning API failure blocks clearance.
- Full 30-minute clearance restarts after API recovery.
- Countdown completion changes status to ELIGIBLE FOR RESUMPTION REVIEW.
- Supervisor confirmation required before activity resumption.

### New Lightning Audit Fields
- Last ≤8 km Detection
- Last 8-15 km Detection
- Clearance Start Time
- Latest Successful Lightning Check
- Supervisor Confirmation Time

### Air Quality Enhancements
- Added NEA 1-Hour PM2.5 API integration.
- Added PM2.5 dashboard tile.
- Added PM2.5 advisory logic.
- Added PM2.5 risk classification.
- Adopted worst-case PSI / PM2.5 risk determination.

### PM2.5 Bands
- 0-55 µg/m³: Normal
- 56-150 µg/m³: Elevated
- 151-250 µg/m³: High
- ≥251 µg/m³: Very High

### Operational Improvements
- Enhanced Outdoor Work Advisory Engine.
- Enhanced Risk Matrix.
- Enhanced Banner Priority Logic.
- Improved management visibility for lightning and haze events.

### Version Summary
v1.7.0 RC1 introduces a production-oriented lightning suspension and resumption workflow with stronger control of activity restart decisions and improved auditability.
