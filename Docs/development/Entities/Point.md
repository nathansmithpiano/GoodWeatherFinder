## Entities: Point

**Point** is the starting point for data in the NWS API.  Each **Location** has at most one **Point**.

A point is found via its GPS coordinates (latitude and longitude) via the following IRI:
```
https://api.weather.gov/points/{latitude},{longitude}
```
<hr>

### Properties

The following uses Mt. Elbert, the highest peak in Colorado, as an example.

| Entity | JSON | Type | Description | Example |
| --- | --- | --- | --- | --- |
| `id` | `id` `properties.@id` | `String` | `primary key` `id` `IRI` | `https://api.weather.gov/points/39.1177,-106.4453` |
| `type` | `type` | `String` | `GeoJSON @type` | `"Feature"` |
| `geometry` | geometry | Geometry (Entity) | Single pair of coordinates | `"type": "Point", "coordinates": [] |
<hr>

- id and properties.@id
	- IRI; primary key & id for this **point**
	- i.e. https://api.weather.gov/points/39.1177,-106.4453
- geometry.coordinates: single set of coordinates; the latitude and longitude for this point and what's used in the IPI (IPI is somewhat less precise)
- properties.cwa: County Warning Area; used in obtaining **forecast(s)**, **forecastGridData**, and **observationStations**

<details><summary><b>JSON</b> <i>Requested May 17 2022</i></summary>

```json
{
    "@context": [
        "https://geojson.org/geojson-ld/geojson-context.jsonld",
        {
            "@version": "1.1",
            "wx": "https://api.weather.gov/ontology#",
            "s": "https://schema.org/",
            "geo": "http://www.opengis.net/ont/geosparql#",
            "unit": "http://codes.wmo.int/common/unit/",
            "@vocab": "https://api.weather.gov/ontology#",
            "geometry": {
                "@id": "s:GeoCoordinates",
                "@type": "geo:wktLiteral"
            },
            "city": "s:addressLocality",
            "state": "s:addressRegion",
            "distance": {
                "@id": "s:Distance",
                "@type": "s:QuantitativeValue"
            },
            "bearing": {
                "@type": "s:QuantitativeValue"
            },
            "value": {
                "@id": "s:value"
            },
            "unitCode": {
                "@id": "s:unitCode",
                "@type": "@id"
            },
            "forecastOffice": {
                "@type": "@id"
            },
            "forecastGridData": {
                "@type": "@id"
            },
            "publicZone": {
                "@type": "@id"
            },
            "county": {
                "@type": "@id"
            }
        }
    ],
    "id": "https://api.weather.gov/points/39.1177,-106.4453",
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [
            -106.4453,
            39.117699999999999
        ]
    },
    "properties": {
        "@id": "https://api.weather.gov/points/39.1177,-106.4453",
        "@type": "wx:Point",
        "cwa": "PUB",
        "forecastOffice": "https://api.weather.gov/offices/PUB",
        "gridId": "PUB",
        "gridX": 33,
        "gridY": 107,
        "forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
        "forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly",
        "forecastGridData": "https://api.weather.gov/gridpoints/PUB/33,107",
        "observationStations": "https://api.weather.gov/gridpoints/PUB/33,107/stations",
        "relativeLocation": {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -106.318985,
                    39.103709000000002
                ]
            },
            "properties": {
                "city": "Twin Lakes",
                "state": "CO",
                "distance": {
                    "unitCode": "wmoUnit:m",
                    "value": 11008.865990169001
                },
                "bearing": {
                    "unitCode": "wmoUnit:degree_(angle)",
                    "value": 278
                }
            }
        },
        "forecastZone": "https://api.weather.gov/zones/forecast/COZ060",
        "county": "https://api.weather.gov/zones/county/COC065",
        "fireWeatherZone": "https://api.weather.gov/zones/fire/COZ220",
        "timeZone": "America/Denver",
        "radarStation": "KGJX"
    }
}
```
</details>