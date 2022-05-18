# Point

Each `Location` has at most one `Point`. Each `Point` has at most one `Location`.  

`Point` is the parent of all other entities and data in both **GoodWeatherFinder** and the **NWS API**. 

`Point` JSON is obtained via its GPS coordinates (latitude and longitude) via the following IRI:<br>
`GET: https://api.weather.gov/points/{latitude},{longitude}`

The following example is for Mt. Elbert, the highest peak in Colorado.<br>
`GET: https://api.weather.gov/points/39.1177,-106.4453`

## Primary Key
The primary key for `Point` is the IRI, included twice in the JSON: `id` and `properties.@id`.  
Both are stored in the entity as it may be helpful for verification later.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java
public class Point {
	private String id; 
	private String propertiesId; 
}
```
</td>
<td>

```json
"id": "https://api.weather.gov/points/39.1177,-106.4453",
"properties": {
    "@id": "https://api.weather.gov/points/39.1177,-106.4453"
```
</td>
</tr>
</tbody>
</table>

## Relationships

### Geometry

Each `Point` has at most one `Geometry`. That `Geometry` has at most one `Coordinates`.  
When `Point` JSON is requested from the NWS API, `Geometry` is updated (replaced) with the current data.

<table padding="0">
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java
public class Point {
	private Geometry geometry;
}
```
```java
public class Geometry {
	private String type;
	private List<Coordinate> coordinateList;
}
```
</td>
<td>

```json
"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}
```
</td>
</tr>
</tbody>
</table>

Each `Point` has 



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