## Point
Primary Key: IRI (String)
Also defined by its coordinates

`Point` has one and only one `Location`



## Location
`Location` 1:1 `Point`

# Alert

#### /alerts
Returns all alerts

#### /alerts/active
Returns all currently active alerts

#### /alerts/active/count
Returns info on the number of active alerts

#### /alerts/active/zone/{zoneId}
Returns active alerts for the given NWS public zone or county

#### /alerts/active/area/{area}
Returns active alerts for the given area (state or marine area)

#### /alerts/types
Returns a list of alert types

#### /alerts/{id}
Returns a specific alert

# Glossary

#### /glossary
Returns glossary terms

# Point

#### /points/{point}
Returns metadata about a given latitude/longitude point

# ForecastOffice

#### /offices/{officeId}
Returns metadata about a NWS forecast office

#### /offices/{officeId}/headlines/{headlineId}
Returns a specific news headline for a given NWS office

#### /offices/{officeId}/headlines
Returns a list of news headlines for a given NWS office

# GridPoint

#### /gridpoints/{wfo}/{x},{y}
Returns raw numerical forecast data for a 2.5km grid area

#### /gridpoints/{wfo}/{x},{y}/forecast
Returns a textual forecast for a 2.5km grid area

#### /gridpoints/{wfo}/{x},{y}/forecast/hourly
Returns a textual hourly forecast for a 2.5km grid area

#### /gridpoints/{wfo}/{x},{y}/stations
Returns a list of observation stations usable for a given 2.5km grid area

# ObservationStations

#### /stations
Returns a list of observation stations.

#### /stations/{stationId}
Returns metadata about a given observation station

#### /stations/{stationId}/observations
Returns a list of observations for a given station

#### /stations/{stationId}/observations/latest
Returns the latest observation for a station

#### stations/{stationId}/observations/{time}
Returns a single observation.

# RadarStation

#### /radar/stations
Returns a list of radar stations

#### /radar/stations/{stationId}
Returns metadata about a given radar station

# Zone

#### /zones
Returns a list of zones

#### /zones/{type}
Returns a list of zones of a given type

#### /zones/{type}/{zoneId}
Returns metadata about a given zone

#### /zones/{type}/{zoneId}/forecast
Returns the current zone forecast for a given zone

#### /zones/forecast/{zoneId}/observations
Returns a list of observations for a given zone

#### /zones/forecast/{zoneId}/stations
Returns a list of observation stations for a given zone
