## Entities: Point

Each **Location** has at most one **Point**.  As such, **Point** is the starting point for obtaining datain in the NWS API. 

A point is found via its GPS coordinates (latitude and longitude) via the following IRI:
```
https://api.weather.gov/points/{latitude},{longitude}
```

The following uses Mt. Elbert, the highest peak in Colorado, as an example.
`https://api.weather.gov/points/39.1177,-106.4453`

<hr>

### Point



```java
// ID and IRI for this Point
private String id; 

// expected to be same as id
private String propertiesId; 
```

```json
"id": "https://api.weather.gov/points/39.1177,-106.4453",
"properties": {
        "@id": "https://api.weather.gov/points/39.1177,-106.4453"
```
		
|



### Properties

The primary key and IRI `String`.<br>
Included twice in the JSON: `id` and `properties.@id`.

```java
private String id; // ID and IRI for this Point
private String propertiesId; // expected to be same as id | saved for verification later
```

```json
"id": "https://api.weather.gov/points/39.1177,-106.4453",
"properties": {
        "@id": "https://api.weather.gov/points/39.1177,-106.4453"
```
<hr>

```java
private String type; // GeoJSON type | i.e. Feature
```

```json
"type": "Feature"
```

```java
public class Point {
	private String propertiesType; // corresponds to other types | used for verification later | i.e. wx:Point
}

public class RelativeLocation {
	private String type;
}
```


```json
"properties": {
	"@type": "wx:Point"
	
"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}
```
<hr>

```java
private String cwa; // County Warning Area | used in IRIs for forecastOffice, forecast, forecastGridData, observationStation
```

```json
"properties": {
	"cwa": "PUB"
```
<hr>

```java
private Geometry geometry; // single pair of Coordinates
```

```json
"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}
```
<hr>

```java

```

```json
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
}
```
<hr>

```java

```

```json

```
<hr>

```java

```

```json

```
<hr>

```java

```

```json

```
<hr>

| Property | JSON | Type | Description | Example |
| --- | --- | --- | --- | --- |
| `id` | `id`<br>`properties.@id` | `String` | `primary key`<br>`IRI` | `id = "https://api.weather.gov/points/39.1177,-106.4453";` |
| `type` | `type`<br>`properties.@type` | `String` | `GeoJSON @type` | `type = "Feature";`<br>`properties.@type = "wx:Point"` |
| `geometry` | `geometry` | `Geometry` | `Coordinates`  | `type = "Point";`<br>`coordinates = [-106.4453,39.117699999999999];` |
| properties.
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