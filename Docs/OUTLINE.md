

Point 1:1 Geometry
Point m:1 ForecastOffice
Point m:1 GridPoint
Point m:2 Forecast
Point m:1 GridPoint
Point m:m ObservationStation
Point m:1 RelativeLocation
Point m:1 ForecastZone
Point m:1 County
Point m:1 FireWeatherZone
Point m:1 TimeZone
Point m:1 RadarStation

ForecastOffice m:m County
ForecastOffice m:m ForecastOffice
Forecast Office ?:m ObservationStation

GridPoint m:1 ForecastOffice
GridPoint m:m ObservationStation



## Point
Primary Key: IRI (String)
Also defined by its coordinates

Each `Point` has one and only one `Location`.
Each `Point` has one and only one `Geometry`.
Each `Point`.`Geometry` has one and only one `Coordinates`.

## Location
Each `Location` has one and only one `Point`.

## Geometry
`Geometry` may have one or many `Coordinates`.
`Geometry` does not need to know about its `Point`.

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
**Used by**
- `Point` *Primary Key*
- `Location` *location.point*

# ForecastOffice

#### /offices/{officeId}
Returns metadata about a NWS forecast office  
**Used by**
- `Point` *point.forecastOffice*
- `ForecastZone` *forecastZone.forecastOffices[]*
- `GridPoint` *gridPoint.forecastOffice*
- `County` *county.forecastOffices[]*
- `FireWeatherZone` *fireWeatherZone.observationStations[]*

#### /offices/{officeId}/headlines/{headlineId}
Returns a specific news headline for a given NWS office

#### /offices/{officeId}/headlines
Returns a list of news headlines for a given NWS office

# GridPoint

#### /gridpoints/{wfo}/{x},{y}
Returns raw numerical forecast data for a 2.5km grid area  
**Used by**
- `Point` *point.forecastGridData*

#### /gridpoints/{wfo}/{x},{y}/forecast
Returns a textual forecast for a 2.5km grid area  
**Used by**
- `Point` *point.forecast*

#### /gridpoints/{wfo}/{x},{y}/forecast/hourly
Returns a textual hourly forecast for a 2.5km grid area  
**Used by**
- `Point` *point.forecastHourly*

#### /gridpoints/{wfo}/{x},{y}/stations
Returns a list of observation stations usable for a given 2.5km grid area  
**Used by**
- `Point` *point.observationStations*
??? Point ObservationStations

# ObservationStations

#### /stations
Returns a list of observation stations.

#### /stations/{stationId}
Returns metadata about a given observation station  
**Used by**
- `ForecastZone` *forecastZone.observationStations[]*
- `ForecastOffice` *forecastOffice.approvedObservationStations*
- `County` *county.observationStations[]*

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
**Used by**
- `Point` *point.forecastZone*
    - confusing, is `forecastZone` a Zone type or is this the same as /zones/{type}/{zoneId}/forecast ?
- `Point` *point.county*
- `Point` *point.fireWeatherZone*
- `FireWeatherZone` *Primary Key*
- `ForecastOffice` *forecastOffice.responsibleCounties*
- `ForecastOffice` *forecastOffice.responsibleForecastZones*
- `ForecastOffice` *forecastOffice.responsibleFireZones*

#### /zones/{type}/{zoneId}/forecast
Returns the current zone forecast for a given zone

#### /zones/forecast/{zoneId}/observations
Returns a list of observations for a given zone

#### /zones/forecast/{zoneId}/stations
Returns a list of observation stations for a given zone
